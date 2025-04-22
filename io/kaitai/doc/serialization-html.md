Serialization Guide
==========

Kaitai Project

Note

 Serialization for Java and Python is made thanks to financial support [from the NLnet Foundation](https://nlnet.nl/project/Kaitai-Serialization).

For a long time, you could only use Kaitai Struct for parsing, not serialization (writing data to file). However, due to high user interest in this feature, we’ve added serialization support to Kaitai Struct.

At the time of writing, it’s only available for Java and Python, but should already work for the vast majority of format specifications. This page explains how to use it. Support for other target languages will follow.

Introduction
----------

While parsing allows you extract data from existing files or byte streams based on the format described by a .ksy specification, serialization has the opposite goal - you know the data and you need to write them to a file in the specified format, which can be read by other applications. This allows several use cases:

1. Editing an existing file. You can parse a file to get the initial data, change the data programmatically and write them back to the same file or another file.

2. Creating a new file from scratch. It’s also possible to start by creating empty objects, then fill them with all the necessary information and finally tell Kaitai Struct to write the object to the provided stream.

Getting started
----------

Once you have the .ksy specification of the format you want to serialize, you need a version of `kaitai-struct-compiler` that supports serialization. The latest 0.10 compiler doesn’t have it yet; you need to build the compiler from source at the moment.

### Building the compiler from source ###

Don’t worry, it should be straightforward:

1. Install `sbt` by following the steps at <https://www.scala-sbt.org/1.x/docs/Setup.html>.

2. Clone the [https://github.com/kaitai-io/kaitai\_struct\_compiler](https://github.com/kaitai-io/kaitai_struct_compiler) repository, checkout the [**serialization**](https://github.com/kaitai-io/kaitai_struct_compiler/tree/serialization) branch.

   ```
   git clone -b serialization https://github.com/kaitai-io/kaitai_struct_compiler.git
   cd kaitai_struct_compiler
   ```

3. Build the compiler using `sbt` that you installed earlier:

   ```
   sbt --error compilerJVM/stage
   ```

   If no error is printed, there should be a compiler build in `jvm/target/universal/stage/bin/kaitai-struct-compiler`. If you run `jvm/target/universal/stage/bin/kaitai-struct-compiler --help`, you should see the `--read-write` option in the usage text:

   ```
   Usage: kaitai-struct-compiler [options] <file>...

     <file>...                source files (.ksy)
     -t, --target <language>  target languages (graphviz, csharp, rust, all, perl, java, go, cpp_stl, php, lua, python, nim, html, ruby, construct, javascript)
     -w, --read-write         generate read-write support in classes (implies `--no-auto-read --zero-copy-substream false`, Java and Python only, default: read-only)

   ```

### Compiling a .ksy specification in read-write mode ###

* Java

* Python

You can compile a .ksy spec to Java classes with serialization support like this:

```
jvm/target/universal/stage/bin/kaitai-struct-compiler --read-write --no-auto-read -t java <ksy-file>
```

You can compile a .ksy spec to Python classes with serialization support like this:

```
jvm/target/universal/stage/bin/kaitai-struct-compiler --read-write --no-auto-read -t python <ksy-file>
```

The most important option is `--read-write`, which enables read-write mode. This adds the methods needed for serialization to the generated classes.

`--no-auto-read` is explicitly specified here for demonstrative purposes. If you omit it, the compiler will still behave as if it were specified, because it’s implied by `--read-write`. Normally in read-only mode, if you don’t specify `--no-auto-read`, you can just use the `fromFile` / `from_file` static method to parse a file and get the object with the extracted data immediately:

* Java

* Python

```
Gif g = Gif.fromFile("path/to/some.gif");
System.out.println("width = " + g.logicalScreen().imageWidth());
```

```
g = Gif.from_file("path/to/some.gif")
print("width = %d" % (g.logical_screen.image_width))
```

Or you can instantiate the `Gif` class directly by invoking the class constructor and passing the stream to read from:

* Java

* Python

```
try (KaitaiStream io = new ByteBufferKaitaiStream("path/to/some.gif")) {
    Gif g = new Gif(io);
    System.out.println("width = " + g.logicalScreen().imageWidth());
}
```

```
with KaitaiStream(open("path/to/some.gif", 'rb')) as _io:
    g = Gif(_io)
    print("width = %d" % (g.logical_screen.image_width))
```

This is because the `_read` method (responsible for parsing the data) is automatically called from constructors of the generated classes, and is also `private` (in Java) because you never need to call it explicitly.

However, in read-write mode, it’s no longer clear to Kaitai Struct why you’re creating a particular object. The purpose may just be to create an empty object to be filled with data and later written, in which case you don’t want to read from any stream. For this reason, `_read` is never called automatically in read-write mode - you need to call it explicitly if you want to read from a stream:

* Java

* Python

```
try (KaitaiStream io = new ByteBufferKaitaiStream("path/to/some.gif")) {
    Gif g = new Gif(io);
    g._read();
    System.out.println("width = " + g.logicalScreen().imageWidth());
}
```

```
with KaitaiStream(open("path/to/some.gif", 'rb')) as _io:
    g = Gif(_io)
    g._read()
    print("width = %d" % (g.logical_screen.image_width))
```

### Installing the runtime library with serialization support ###

As with the compiler, the latest released 0.10 KS runtime libraries don’t have serialization capabilities yet.

* Java

* Python

In Java, you need to checkout the [https://github.com/kaitai-io/kaitai\_struct\_java\_runtime](https://github.com/kaitai-io/kaitai_struct_java_runtime) repo:

```
git clone https://github.com/kaitai-io/kaitai_struct_java_runtime.git
cd kaitai_struct_java_runtime
```

The runtime library is a dependency of all Java code generated by `kaitai-struct-compiler`, so you have to build it and make it available to your generated Java "format library" at compile time. If you use [Maven](https://maven.apache.org/), run this command in the `kaitai_struct_java_runtime` directory to build it and install it to your local Maven repository:

```
mvn install
```

Note

If the `gpg` command isn’t available on your system, `mvn install` will fail because of `maven-gpg-plugin` used to sign artifacts when publishing. In that case, comment this plugin in `pom.xml` like this:

```
      </plugin>
      <!-- <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-gpg-plugin</artifactId>
        <version>1.5</version>
        <executions>
          ...
        </executions>
      </plugin> -->
    </plugins>
  </build>
```

Now you can include the serialization-capable Java runtime library in your project like this:

```
    <dependency>
      <groupId>io.kaitai</groupId>
      <artifactId>kaitai-struct-runtime</artifactId>
      <version>0.11-SNAPSHOT</version>
    </dependency>
```

But note that the `0.11-SNAPSHOT` version only exists in your local Maven repository (`~/.m2`) after you ran `mvn install` in the Java runtime library folder.

In Python, you need to install the runtime library from the [https://github.com/kaitai-io/kaitai\_struct\_python\_runtime](https://github.com/kaitai-io/kaitai_struct_python_runtime) repo. You can do it with [pip](https://pypi.org/project/pip/) (package installer for Python); you also need [Git](https://git-scm.com/) while running the command because the installation involves cloning the source code from GitHub:

```
python -m pip install -U --pre git+https://github.com/kaitai-io/kaitai_struct_python_runtime.git
```

After that, you can import the serialization-capable `KaitaiStream` class defined in the runtime library like this (generated modules do it too):

```
from kaitaistruct import KaitaiStream
```

For brevity, this import will be omitted from code snippets later in this guide, but it’s often needed.

General serialization procedure
----------

Let’s start with a simple example to see how the serialization can be used. First, we compile the following .ksy specification in read-write mode:

```
meta:
  id: hello_world
  endian: le
seq:
  - id: foo
    type: s4
    repeat: expr
    repeat-expr: 2
```

This will generate a `HelloWorld.java` / `hello_world.py` source file with class `HelloWorld`. We want to set `foo` to `[-4, 65536]` and write the structure to bytes. This is how we do it:

* Java

* Python

```
HelloWorld hw = new HelloWorld();
hw.setFoo(new ArrayList<>(Arrays.asList(-4, 65536)));
hw._check();

byte[] output = new byte[8];
try (KaitaiStream io = new ByteBufferKaitaiStream(output)) {
    hw._write(io);
}
// output: [fc ff ff ff 00 00 01 00]
```

```
hw = HelloWorld()
hw.foo = [-4, 65536]
hw._check()

_io = KaitaiStream(io.BytesIO(bytearray(8)))
hw._write(_io)

output = _io.to_byte_array()
# output: [fc ff ff ff 00 00 01 00]
```

Note that there are essentially 4 phases of serialization:

1. Initialize an object instance of a KS-generated class (which reflects a user-defined type in the source .ksy specification).

2. Set the object properties (`seq` fields or positional `instances` in the .ksy) according to the data you want to serialize.

3. Call the `_check` method of the KS object after setting its properties once it’s ready for serialization.

4. Call the `_write` method on the top-level object and pass the `KaitaiStream` object you want to write to.

First, we create an empty instance of the top-level class `HelloWorld` and bind it to the `hw` variable. As you can see in the original .ksy spec, it has only one field called `foo`, which is a list of two `s4` (signed 4-byte) integers. We assign such list with the values we wanted to write to the `foo` field (using the `setFoo` setter in Java or just by setting the field in Python). After that, we believe that the `hw` object is ready to be written, so we call `hw._check()`. When it passes, we move on to the actual writing.

* Java

* Python

We prepare a byte array for the output, create a `ByteBufferKaitaiStream` as a wrapper around this byte array and then call the `_write` method on the top-level `hw` object, which serializes it into the provided stream. After the `try`-with-resources statement, `output` holds the final byte data that we can, for example, write to a file or transfer over the network.

We create a `KaitaiStream` backed by a `BytesIO` object for the output and then call the `_write` method on the top-level `hw` object, which serializes it into the provided stream. After that, we call the `to_byte_array` method on the `KaitaiStream`. This gives us the final byte data that we can, for example, write to a file or transfer over the network.

### Consistency checks: the `_check` method ###

Let’s focus on what the `_check` method does. We know that `foo` is expected to be a list of exactly 2 integers (because of `repeat-expr: 2` in the source .ksy). Every parsing of the `hello_world` type tries to read 2 integers, and in any successfully parsed `HelloWorld` object, `foo` will be always 2 elements long. However, the `setFoo` setter allows us to set *any* integer list - even if its length is 0, 1 or greater than 2.

Nevertheless, if we set `foo` to a list of length other than 2 and write the `hw` object to bytes, we won’t be able to get the same state of the `HelloWorld` object by parsing these bytes again: either the parsing fails with an EOF exception if the stream was shorter than 8 bytes, or we get garbage values in `foo` (if we attempted to write `foo` with less than 2 elements) because we interpret some bytes outside `foo` as if they were `foo` values, or we may read 2 correct values, but the object we serialized had actually more. In such cases, it’s very much possible that not only the parsed `foo` wouldn’t match the `foo` we wrote, but also the offsets of **all** fields after `foo` would be shifted, so their values would be incorrect too.

This is because by setting `foo` to anything other than a 2-integer list, we violate the property of **consistency** - the data is not consistent with the constraints directly following from how the format is specified in the source .ksy file. Kaitai Struct knows these constraints, and generates assertions for them in the `_check` method whenever possible. If `_check` detects a consistency issue, it throws a `ConsistencyError`, telling you to fix the problem and try again. This protects you from proceeding to the writing phase with inconsistent values, which would inevitably result into corrupt data that cannot be faithfully decoded back to the original values.

To see it in action, let’s try what happens if we set `foo` to a list of length 3 and ask the `HelloWorld` class what it thinks about the consistency of this object:

* Java

* Python

```
HelloWorld hw = new HelloWorld();
hw.setFoo(new ArrayList<>(Arrays.asList(-4, 65536, 128)));
hw._check(); // io.kaitai.struct.ConsistencyError: Check failed: foo, expected: 2, actual: 3
```

```
hw = HelloWorld()
hw.foo = [-4, 65536, 128]
hw._check()  # kaitaistruct.ConsistencyError: Check failed: foo, expected: 2, actual: 3
```

As expected, the `_check` method caught the problem and threw an exception - the expected length of field `foo` was 2, but it was 3, which doesn’t match the format definition.

Notes on individual features
----------

### User-defined types ###

Real-world .ksy specifications often define custom types in the `types` section. For example:

```
meta:
  id: user_types
  endian: le
seq:
  - id: one
    type: chunk
types:
  chunk:
    seq:
      - id: len_body
        type: u4
      - id: body
        size: len_body
```

A typical way to serialize such format would be as follows:

* Java

* Python

```
UserTypes ut = new UserTypes();

UserTypes.Chunk one = new UserTypes.Chunk(null, ut, ut._root());
one.setLenBody(2);
one.setBody(new byte[] { 'h', 'i' });
one._check();

ut.setOne(one);
ut._check();

byte[] output = new byte[6];
try (KaitaiStream io = new ByteBufferKaitaiStream(output)) {
    ut._write(io);
}
// output: [02 00 00 00 68 69]
```

```
ut = UserTypes()

one = UserTypes.Chunk(None, ut, ut._root)
one.len_body = 2
one.body = b"hi"
one._check()

ut.one = one
ut._check()

_io = KaitaiStream(io.BytesIO(bytearray(6)))
ut._write(_io)

output = _io.to_byte_array()
# output: [02 00 00 00 68 69]
```

First, we instantiate the root class `UserTypes` as usual. Then we need the instance of the user-defined `chunk` type, translated as `UserTypes.Chunk` in Java or Python. We use the usual way to create an instance of a class, but this time using all 3 arguments of the constructor:

* Java

* Python

```
        public Chunk(KaitaiStream _io, UserTypes _parent, UserTypes _root) {
            // ...
        }
```

```
    class Chunk(ReadWriteKaitaiStruct):
        def __init__(self, _io=None, _parent=None, _root=None):
            # ...
```

The reason is that we must provide values for the `_parent` and `_root` parameters (see [their description](user_guide.html#usertype-methods) in the User Guide). These built-in references should be valid in all KS types so that it’s possible to rely on them in expressions inside the .ksy spec when needed. When you instantiate inner objects (any object instances of user-defined types other than the root object) manually, you have to set these properties correctly.

Note the generally-applicable rule of what should go there (let’s call the parent object as `*p*`):

* `*p*` to `_parent` (in this case, `one`'s parent object is `ut` because we’re doing `ut.setOne(one)` / `ut.one = one` later),

* `*p*._root()` / `*p*._root` to `_root`.

If you don’t set the correct values to both `_parent` and `_root`, it’s a consistency issue that will be reported in `_check` of the parent object (`ut` in this case):

* Java

* Python

```
UserTypes ut = new UserTypes();

UserTypes.Chunk one = new UserTypes.Chunk(null, ut); // WRONG: we didn't pass "ut._root()" to "_root"!
one.setLenBody(2);
one.setBody(new byte[] { 'h', 'i' });
one._check();

ut.setOne(one);
ut._check(); // io.kaitai.struct.ConsistencyError: Check failed: one, expected: org.example.UserTypes@539645a2, actual: null
```

```
ut = UserTypes()

one = UserTypes.Chunk(None, ut)  # WRONG: we didn't pass "ut._root" to "_root"!
one.len_body = 2
one.body = b"hi"
one._check()

ut.one = one
ut._check()  # kaitaistruct.ConsistencyError: Check failed: one, expected: <user_types.UserTypes object at 0x0000017A19626610>, actual: None
```

Note

The error message is a bit inconcrete at the moment, because it only says there’s a problem with the field `one` but doesn’t specify what exactly it is. This will be improved in the future, but for now, check out the line where the `ConsistencyError` was thrown for more details:

* Java

* Python

```
io.kaitai.struct.ConsistencyError: Check failed: one, expected: org.example.UserTypes@539645a2, actual: null
    at org.example.UserTypes._check (UserTypes.java:48)
    ...
```

```
public class UserTypes extends KaitaiStruct.ReadWrite {
    // ...
    public void _check() {
        if (!Objects.equals(one()._root(), _root()))
            throw new ConsistencyError("one", one()._root(), _root());
        // ...
    }
```

```
Traceback (most recent call last):
  File "C:\main.py", line 11, in <module>
    ut._check()
  File "C:\user_types.py", line 34, in _check
    raise kaitaistruct.ConsistencyError(u"one", self.one._root, self._root)
kaitaistruct.ConsistencyError: Check failed: one, expected: <user_types.UserTypes object at 0x0000017A19626610>, actual: None
```

```
class UserTypes(ReadWriteKaitaiStruct):
    # ...
    def _check(self):
        pass
        if self.one._root != self._root:
            raise kaitaistruct.ConsistencyError(u"one", self.one._root, self._root)
        # ...
```

By looking into the generated code, we figure out that the `_root` parameter of field `one` had a wrong value. It should have been equal to `ut._root`, but it was `null` / `None`.

After we create an instance of the `UserTypes.Chunk` subtype, we set its properties, and then we **call `_check`**. This is important: `_check` always works only for the one object on which you call it, it doesn’t recursively descend into substructures (unlike `_read` and `_write` which do that, so you call them just on the top-level object). So it’s **not enough** to call `_check` just on the top-level object - you have do it for every KS object on which you use setters.

* Java

* Python

```
UserTypes ut = new UserTypes();

UserTypes.Chunk one = new UserTypes.Chunk(null, ut, ut._root());
one.setLenBody(2);
one.setBody(new byte[] { 'h', 'i' });
one._check();

ut.setOne(one);
ut._check();

// ...
```

```
ut = UserTypes()

one = UserTypes.Chunk(None, ut, ut._root)
one.len_body = 2
one.body = b"hi"
one._check()

ut.one = one
ut._check()

# ...
```

### Fixed contents and validated fields ###

After creating a new KS object, you must also set fields with `contents` or `valid` on them, even if there’s only one valid value they can have. Kaitai Struct doesn’t set them automatically at the moment. For example, the following `magic` field

```
meta:
  id: elf
  # ...
seq:
  - id: magic
    contents: [0x7f, "ELF"]
```

needs to be set as follows:

* Java

* Python

```
Elf e = new Elf();

e.setMagic(new byte[] { 0x7f, 'E', 'L', 'F' });
// ...
e._check();
```

```
e = Elf()

e.magic = b"\x7fELF"
# ...
e._check()
```

The `_check` method validates such fields, so you get notified if the values are not valid.

### Value instances ###

They don’t have setters. If you need to make value instances change, you have to set their inputs (fields they depend on). For example:

```
meta:
  id: value_instances
seq:
  - id: len_data_raw
    type: u1
  - id: data
    size: len_data
instances:
  len_data:
    value: len_data_raw - 3
```

* Java

* Python

```
ValueInstances r = new ValueInstances();

r.setData(new byte[] { 1, 2, 3, 4, 5 });
r.setLenDataRaw(8);
System.out.println(r.lenData()); // => 5
```

```
r = ValueInstances()

r.data = b"\x01\x02\x03\x04\x05"
r.len_data_raw = 8
print(r.len_data)  # => 5
```

We set a 5-byte array to `data`, so for the object to be consistent, we need `len_data` to be `5`. Since it’s defined as `len_data_raw - 3`, we set `len_data_raw` to `8`, which makes `len_data` to be `8 - 3 = 5`.

What happens if you want to change the length of `data` in this existing object? Instances in KS are cached, so even if you change `len_data_raw`, `len_data` will keep returning the old cached value (`5`):

* Java

* Python

```
// ...
System.out.println(r.lenData()); // => 5

r.setData(new byte[] { 1, 2, 3 });
r.setLenDataRaw(6);
System.out.println(r.lenData()); // => 5 (!)
```

```
# ...
print(r.len_data)  # => 5

r.data = b"\x01\x02\x03"
r.len_data_raw = 6
print(r.len_data)  # => 5 (!)
```

To fix this, you need to call a special method `_invalidate{Inst}` (`_invalidate_{inst}` in Python) associated with the value instance after changing `len_data_raw`:

* Java

* Python

```
// ...
System.out.println(r.lenData()); // => 5

r.setData(new byte[] { 1, 2, 3 });
r.setLenDataRaw(6);
r._invalidateLenData();
System.out.println(r.lenData()); // => 3
```

```
# ...
print(r.len_data)  # => 5

r.data = b"\x01\x02\x03"
r.len_data_raw = 6
r._invalidate_len_data()
print(r.len_data)  # => 3
```

The Java’s `_invalidate{Inst}` / Python’s `_invalidate_{inst}` method invalidates the cached value of the instance so that it’s recalculated on the next access.

### Parse instances ###

They have setters and their own `_check{Inst}` (`_check_{inst}`) method which you should call. Additionally, you can also use a special boolean `set{Inst}_ToWrite` setter (in Python you’d assign a boolean to a property `{inst}__to_write`), allowing you to disable writing of a specific instance (as `r.set{Inst}_ToWrite(false)` in Java, or `r.{inst}__to_write = False` in Python) in a particular KS object. This may be useful for C-style `union` members (several overlapping fields with different types, but only one applies in any object), lookaheads or other positional instances you don’t want to write.

### Parameters ###

You can give them to the constructor when instantiating the KS type and you can later change them via setters. Again, KS doesn’t set almost anything automatically, so you’re usually in charge of setting all parameters, even though you need to set the parameters to same values that the parent type would pass to them. The `_check` method of the parent type contains checks whether this holds.

Note

 A known issue is that there’s no setter for the built-in `_is_le` parameter used to inherit the [calculated default endianness](user_guide.html#calc-endian) from a parent type, so if you want to change it in an existing object, for the time being you need to recreate the object with the correct `_is_le` passed to the constructor, or use reflection to set this private field. This will be improved later.

#### Stream parameters ####

The only parameters you normally don’t set are parameters of base type `io` (a KaitaiStream-compatible I/O stream). These are declared as `type: io` or `type: io[]`. They are set automatically by the generated serialization code in inner objects (objects with a parent object). However, if your root object has a stream parameter, you have to set it yourself, because Kaitai Struct has no way of knowing what to pass there (the invocation of the root object obviously isn’t in the .ksy spec).

Streams passed as parameters to the top-level object also require special attention. When you call `r._write()` on the root object `r`, substreams of the `r`'s stream will be collapsed to it. However, this won’t happen for the unconnected streams added externally via parameters, because they’re not in the normal hierarchy of streams under the root stream (and the `_write` method that you call knows directly only about the root stream, so it can only flatten *its* substreams). So for every external stream, you have to manually call `extIo.writeBackChildStreams()` in Java / `ext_io.write_back_child_streams()` in Python after invoking `r._write()` on the root object.

### Lengths and offsets ###

Current serialization support relies on fixed-length streams, meaning that once you create a stream, it’s not possible to resize it later. Therefore, you’ll often need to calculate sizes "manually" in your application along with setting the object properties (at least for the root stream, which you have to provide to the `_write` method). The recommended way to do that is outlined in [this GitHub comment](https://github.com/kaitai-io/kaitai_struct/issues/27#issuecomment-1358689992).

### Enums ###

Enum values not present in the enum definition are not supported in Java or Python right now. An attempt to write them causes `NullPointerException` in Java, `AttributeError` in Python.

### Bit-sized integers ###

Unlike the existing parser implementation of bit types which relied on explicit `alignToByte()` calls (and this resulted in many problems, because in many cases the compiler failed in where to insert them and where not), all byte-aligned operations in Java and Python runtime libraries with serialization support now perform the byte alignment automatically, and the explicit `alignToByte()` calls shouldn’t be needed anymore.

When you write a structure with `X`-bit `type: bX` fields, only full bytes are written once they’re known. This means that if your format ends at an unaligned bit position, the bits of the final partial byte remain in the internal "bit buffer", but they will not be written to the underlying stream until you do some operation which aligns the position to a byte boundary (e.g. `writeBytes(0)`, `seek(…​)`, or explicit `writeAlignToByte()`). However, if you don’t have anything else to write and don’t need to work with that stream anymore, it’s recommended to `close()` the stream, which automatically writes the remaining bits (if any) before closing the stream.

* Java

* Python

This is why you should use the `try`-with-resources statement to create and manage the stream, as you saw in previous examples:

```
try (KaitaiStream io = new ByteBufferKaitaiStream(output)) {
    hw._write(io);
}
```

It calls `close()` automatically at the end of the `try`-with-resources block, so you don’t have to think about it.

In Python, the feature of `KaitaiStream.close()` that it flushes unwritten bits is effectively only meaningful for **file** streams. This is because the in-memory `BytesIO` stream (see [**io.BytesIO**](https://docs.python.org/3/library/io.html#io.BytesIO) in Python docs) discards the underlying bytes buffer when the `close()` method is called. Once `BytesIO.close()` is called (which `KaitaiStream.close()` *does* call), you lose all data associated with the `BytesIO` object. So any data must be exported from the `BytesIO` before it’s closed.

Note

It’s not even that important to close `BytesIO` streams. `BytesIO.close()` only frees the memory of its buffer, which is something that the garbage collector would do anyway when the `BytesIO` object becomes inaccessible.

And when it comes to freeing memory early, calling `close()` of the root stream would help only partially, because it has no effect on substreams, which often duplicate large chunks of the root stream in memory (at least until [zero-copy substreams](https://github.com/kaitai-io/kaitai_struct/issues/44) are implemented). So it’s better to wait for the whole KS object to get garbage-collected, which will deal with both the root stream and substreams.

In contrast, file streams (typically from the [**open()**](https://docs.python.org/3/library/functions.html#open) function) **need** to be closed, especially if you have been writing to them. See the section [7.2. Reading and Writing Files](https://docs.python.org/3/tutorial/inputoutput.html#reading-and-writing-files) in the official Python tutorial (`f` is a [file object](https://docs.python.org/3/glossary.html#term-file-object) previously returned by [**open()**](https://docs.python.org/3/library/functions.html#open)):

>
>
>
>
> **Warning**: Calling `f.write()` without using the `with` keyword or calling `f.close()` **might** result in the arguments of `f.write()` not being completely written to the disk, even if the program exits successfully.
>
>
>
>

So from the KS perspective, the recommendations are the following:

* If you use `BytesIO` to create the root `KaitaiStream` object, you don’t need to call `close()` or use the `with` keyword to call it automatically. After you write the KS object to the stream, use the `to_byte_array()` method of `KaitaiStream` to convert the stream to bytes, as you saw in previous code snippets:

  ```
  _io = KaitaiStream(io.BytesIO(bytearray(8)))
  hw._write(_io)

  output = _io.to_byte_array()
  ```

  This method works even if the format ends at an unaligned bit position - the `to_byte_array()` method implicitly aligns the stream position to a byte boundary, so the buffered bits are flushed before the bytes are exported.

* If you use a [file object](https://docs.python.org/3/glossary.html#term-file-object) (typically from [**open()**](https://docs.python.org/3/library/functions.html#open)) to initialize the `KaitaiStream`, it’s best to use the `with` keyword to manage the stream. But given that `KaitaiStream` relies on being fixed-length, note that the file must already have the final size once you pass it to `KaitaiStream` (the `KaitaiStream` object currently remembers the stream size at creation time and won’t allow `write*()` methods to exceed it). You can use [**truncate()**](https://docs.python.org/3/library/io.html#io.IOBase.truncate) to set the file length. Like this:

  ```
  f = open('path/to/file.bin', 'wb')  # use io.open() instead if you care about Python 2 compatibility
  f.truncate(8)

  with KaitaiStream(f) as _io:
      hw._write(_io)
  ```

  Note that it’s not necessary to manage the file object using the `with` keyword too - `KaitaiStream` consumes the given underlying I/O stream (in this case the file object `f`) and takes care of closing it once it’s being closed itself.

### Consistency checks that cannot be done in `_check` ###

Sometimes a consistency check cannot be performed in `_check` because the user expressions from the .ksy specification that the check needs to use do not allow it. A typical example is when the expression makes use of the built-in `_io` variable, for example:

```
seq:
  - id: rest
    size: _io.size - _io.pos
```

Since it’s a fixed-length byte array with the `size` expression denoting its length, it’s necessary to check whether the length of the `rest` byte array (that might have been changed via a setter) and the value of the `size` expression `_io.size - _io.pos` match. But this expression uses `_io`, so it cannot be performed in `_check`: `_check` is meant to check pure data consistency and the `_io` may not be available at this point. So this consistency check will be moved to `_write` just before the `rest` field would be written.
