Kaitai Struct: Java notes
==========

Source files generation
----------

To use Kaitai Struct specifications in Java, one must compile .ksy
specs to .java classes implementing parsing/serialization logic first:

* This can be done manually: by [invoking kaitai-struct-compiler directly](user_guide.html#invocation), and adding generated files to
  your project.

* For certain build pipelines, the process can be automated by
  introducing this generation step into build flow:

  * for [Apache Maven](https://maven.apache.org): [kaitai-maven-plugin](https://github.com/valery1707/kaitai-maven-plugin)

  * for [Gradle](https://gradle.org): [kaitai-gradle-plugin](https://github.com/valery1707/kaitai-gradle-plugin)

Usage patterns
----------

Parsing a structure directly from a local file:

```
AnExampleClass.fromFile("an_example.data")
```

Parsing a structure from a byte array (`byte[]`):

```
new AnExampleClass(new KaitaiStream(byteArray))
```

Note that parsing from non-seekable streams (i.e.[FileInputStream](https://docs.oracle.com/javase/7/docs/api/java/io/FileInputStream.html),[BufferedInputStream](https://docs.oracle.com/javase/7/docs/api/java/io/BufferedInputStream.html),
etc) is not supported and probably won’t be supported, as a lot of
parsing functionality in KS relies on seek support.

Runtime library
----------

### Installation ###

Generated code for Java relies on[Kaitai Struct runtime library for Java](https://github.com/kaitai-io/kaitai_struct_java_runtime). It is a small, MIT-licensed library, which
is[published in Maven Central Repository](https://central.sonatype.com/artifact/io.kaitai/kaitai-struct-runtime), so typically it’s enough to add the
following to one’s `pom.xml`:

```
<dependency>
    <groupId>io.kaitai</groupId>
    <artifactId>kaitai-struct-runtime</artifactId>
    <version>0.11</version>
</dependency>
```

For other build tools, such as Ivy, SBT, Gradle, Leiningen, Buildr,
etc, please consult Central Repository’s page for exact instructions.

Alternatively, one can just copy whole source code to one’s project: the
library is intentionally kept small and has no external dependencies, so
it should be easy enough as well.

### API ###

Following most other runtimes example, everything revolves around two
basic classes:

* KaitaiStruct — a common superclass for all classes that represent
  user types in KS. Java implementation is very limited and basically
  only keeps `_io` member of type KaitaiStream and provides a getter
  for it.

* KaitaiStream — a useful abstraction of seekable input stream that
  can be read with [Kaitai Struct stream API](stream_api.html)(i.e. methods like `readU4le()`. Internally, it uses a[ByteBuffer](https://docs.oracle.com/javase/7/docs/api/java/nio/ByteBuffer.html)(either a[MappedByteBuffer](https://docs.oracle.com/javase/7/docs/api/java/nio/MappedByteBuffer.html)backed by[FileChanel](https://docs.oracle.com/javase/7/docs/api/java/nio/channels/FileChannel.html)for parsing local files, or a regular wrapper over a given byte
  array), so it can work on both local files and in-memory data.

Naming
----------

KS tries to follow mandatory and recommended Java practices as close as
possible.

Class names would be represented in upper camel case (i.e.`an_example_class` ⇒ `AnExampleClass`).

All attributes and instance names use lower camel case (i.e.`an_example_attribute` ⇒ `anExampleAttribute`).

Types
----------

All user types are mapped 1-to-1 to relevant Java classes. Nested types
are mapped to nested classes, i.e. for nested types like this:

```
meta:
  id: parent
# ...
types:
  child:
    # ...
    types:
      grandchild:
        # ...
```

one can expect to get the following class structure:

```
public class Parent extends KaitaiStruct {
    public static class Child extends KaitaiStruct {
        public static class GrandChild extends KaitaiStruct {
        }
    }
}
```

Every generated class will have 3 constructors and a static factory
method (plus a private `_read()` method that is invoked from all the
constructors to do actual parsing):

```
public AnExampleClass(KaitaiStream _io)
public AnExampleClass(KaitaiStream _io, KaitaiStruct _parent)
public AnExampleClass(KaitaiStream _io, KaitaiStruct _parent, AnExampleClass _root)
public static AnExampleClass fromFile(String fileName)
```

Attributes
----------

Sequence attribute parsing is done in `_read()` method which is
typically invoked from a constructor. All parsed attributes are stored
as private member variables.

For all attributes, a relevant getter method will be generated, so an
attribute can be accessed outside of class like`classInstance.anExampleAttribute()`.

Instances
----------

TODO

Enums
----------

TODO

Primitive type mapping
----------

There are several things of note that influence mapping KS types to Java
types:

* There are no support for unsigned integer types in Java. In some cases
  it’s no big deal, but some use cases (for example, comparison or bit
  shifts) may be severely hindered by that issue. KS tries to make up for
  that fact by using larger signed types where that’s possible and
  reasonable to do. Where it’s not possible (i.e. 64-bit unsigned integers
  — `u8`), KS would use signed `long` type.

* Java has 2 types for every numeric type: "primitive" type (i.e. `int`)
  and "reference" type (i.e. `Integer`) — the latter being a full-featured
  object that can have `null` assigned to it and stored in collections.
  It’s not practical to use reference types everywhere, so KS makes use of
  them only in the following situations:

* when data type is used as part of a collection

* when it’s possible that a particular attribute / instance will be
  unassigned (i.e. because of [[if|attribute description#if]] expression)
  — `null` will be returned in this case

The overall primitive type mapping goes as follows:

|   `type`    |Java primitive type|Java reference type|
|-------------|-------------------|-------------------|
|   no type   |      byte[]       |      byte[]       |
|    `u1`     |        int        |      Integer      |
|    `u2`     |        int        |      Integer      |
|    `u4`     |       long        |       Long        |
|    `u8`     |       long        |       Long        |
|    `s1`     |       byte        |       Byte        |
|    `s2`     |       short       |       Short       |
|    `s4`     |        int        |      Integer      |
|    `s8`     |       long        |       Long        |
|`str`, `strz`|      String       |      String       |

### String encoding ###

Encoding a stream of bytes into a `String` is done with the standard
Java API:[String method constructor](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#String(byte%5B%5D,%20java.nio.charset.Charset))

Array types
----------

All repetitions in Java are translated to `ArrayList<~>`
