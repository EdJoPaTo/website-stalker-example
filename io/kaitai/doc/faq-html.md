Kaitai Struct: FAQ
==========

General
----------

### Is it fast? ###

Yes, pretty much. Kaitai Struct is not a runtime interpreter, but a
compiler — thus it imposes no additional runtime performance penalty.
Code that it generates is about as fast as one can write in a particular
language to parse a certain data format.

That said, note that Kaitai Struct is all about producing a clean API for
parsing binary data. That means that general usage plan is:

1. Create object (structure) in memory and parse stream into it

2. Use it via API afterwards

This pattern is generally a good fit for most applications, but for some
types of workloads you might want a completely different approach: acting
as soon as every particular chunk of data stream is parsed based on that
chunk only. This calls for an event-based parsing model (i.e. you define
some code that will be executed on each particular state of the parser)
and thus, probably, you’ll find that other tools like[parser combinators](https://en.wikipedia.org/wiki/Parser_combinator),
finite-state machine generators or even plain[lexer/parser generators](https://en.wikipedia.org/wiki/Comparison_of_parser_generators) will suit that approach better than Kaitai Struct. In these
cases, Kaitai Struct’s approach "read-then-use" **might** be slower than
event-based "read-and-act-simultaneously" approach.

### Is output of KS readable? ###

Yes, Kaitai Struct compiler generates very human-readable files, which can be examined with naked eye, debugged if needed, etc. For example, reading a two-byte signed little-endian integer is usually translated into something like:

```
field = _io.readS2Le();
```

### Does it support writing (generation, serialization) of structures into stream, or only reading (parsing, deserialization) of structures from the stream? ###

So far Kaitai Struct focuses on reading (parsing) only. There are plans to support writing, but don’t hold your breath for it — it’s a pretty major change and it’ll probably happen after 1.x.

There is a[relevant issue in our issue tracker](https://github.com/kaitai-io/kaitai_struct/issues/27), which sports a proof-of-concept compiler branch
that has some writing support (Java only).

### Does it support `mmap` (memory-mapped) to access files? ###

Some languages runtimes support so-called "memory mapped" files. The
idea is simple: using OS-provided mechanism, one marks up a certain
memory area to reflect exactly contents of a file. After that, one can
parse the file by accessing that memory area (as it would be using
normal in-memory buffer).

Right now, mmap support is available:

* In Java — by using [ByteBufferKaitaiStream](https://github.com/kaitai-io/kaitai_struct_java_runtime/blob/master/src/main/java/io/kaitai/struct/ByteBufferKaitaiStream.java)

* in C# — by:

  * opening a file using [MemoryMappedFile](https://docs.microsoft.com/en-us/dotnet/api/system.io.memorymappedfiles.memorymappedfile?view=netframework-4.8) object

  * calling [MemoryMappedFile.CreateViewStream](https://docs.microsoft.com/en-us/dotnet/api/system.io.memorymappedfiles.memorymappedfile.createviewstream?view=netframework-4.8#System_IO_MemoryMappedFiles_MemoryMappedFile_CreateViewStream) method on it to get [MemoryMappedViewStream](https://docs.microsoft.com/en-us/dotnet/api/system.io.memorymappedfiles.memorymappedviewstream?view=netframework-4.8)

  * passing that MemoryMappedViewStream as a Stream into a KaitaiStream constructor

* In all other languages — by invoking mmap operation manually
  (getting a pointer to in-memory buffer), and then wrapping that
  buffer into KaitaiStream

Note that memory-mapped files are not "the silver bullet" and have
both their pros and cons, namely:

* Organizing a memory map is relatively slow operation in comparison
  to simple file opening. If you want to process lots of small files,
  chances are memory-mapped approach would be slower just because of
  the per-file mmap overhead.

* Memory-mapped files work by specifying exact file size to do a
  memory map operation. File size must be known a priori and must
  remain constant during the parsing timeframe. That means that one
  can’t use mmap on:

  * Files that get appended to during parsing, i.e. live packet capture
    stream file, live log files, etc

  * Virtual files on unknown size (such as majority of Linux procfs /
    sysfs files)

* Concurrent access of different processes to the same file using mmap
  might be non-trivial.

How does it compare to …​
----------

### …​ Python library Construct? ###

Actually, Construct is the closest analog to Kaitai Struct. It is also a declarative and symmetric binary parsing library, but there are significant differences:

* Construct does both parsing and serialization, instead of only parsing ([feature #27](https://github.com/kaitai-io/kaitai_struct/issues/27)).

* Construct is a Python-only module, instead of supporting multiple languagues.

* Construct is "declarative" in sense that it defines data structures instead of parsing code. The structures are still defined using Python language, instead of YAML.

* Construct aims at offering more sophisticated building blocks, including those only available on Python like Pickle and Numpy protocols, instead of most basic/common elements.

In fact, there is an open and active collaboration between Construct and Kaitai Struct. There are (currently being implemented) import/export tools, that allow translating schemes between the two frameworks.

Main documentation site: <https://construct.readthedocs.io/en/latest/>

### …​ Google Protocol Buffers, ASN.1, Apache Thrift, Apache Avro, BSON, MessagePack, Microsoft Bond, Hessian, ZeroC ICE, etc? ###

In short: these projects and Kaitai Struct solve completely different
problems.

Protobuf, ASN.1, Apache Thrift, etc, are designed to take a certain
block of data in memory, serialize it, transfer to other system, and
deserialize it there. Binary representation is driven by the data and
encoded according to particular standard of a given protocol, which
usually has a fixed representation for integers, for strings, for
arrays, for dictionaries, etc. Most of these project allow generated
formats to be automatically extensible, carry versioning information,
automatically embed typing information of some sort, etc.

However, you can’t read an arbitrary binary format (like, for example,`.gif`, `.wav`, or `.zip`) with any of these tools, and they’re not
really architected to do that job.

KS approach is almost the exact opposite: given some sort of existing
(or planned) binary representation, build a set of classes that the
data inside this representation can be held in and generate a parser
for it.

You can totally read an arbitrary binary format (or enjoy diverse
library of ready-made format specifications, including[.gif](//formats.kaitai.io/gif/),[.wav](//formats.kaitai.io/wav/) and[.zip](//formats.kaitai.io/zip/)). To some extent, you can use KS
in a task "send block of data from point A to point B", if you prefer
to have more control over your serialization scheme — but, obviously,
you’ll have to add features like backwards compatibility, versioning,
etc, in your protocol manually.

So, to summarize:

* "Have data in memory, need binary protocol" ⇒ use Protobuf & company

* "Have binary protocol, need data in memory" ⇒ use Kaitai Struct

Note that you can actually use Kaitai Struct to parse most of the
mentioned protocols. It will typically give you many low-level
implementation details, which you might care about if you’re interested
in digital forensics (DFIR) or digital preservation. You can find some
of these protocols already specified under "Serialization Protocols"
section in [Kaitai Struct Format Gallery](//formats.kaitai.io/).

Software mentioned

* [Google Protocol Buffers](https://github.com/protocolbuffers/protobuf)

* [ASN.1](https://en.wikipedia.org/wiki/Abstract_Syntax_Notation_One)

* [Apache Thrift](https://thrift.apache.org/)

* [Apache Avro](https://avro.apache.org/)

* [BSON](http://bsonspec.org/)

* [MessagePack](https://msgpack.org/)

* [Microsoft Bond](https://github.com/Microsoft/bond)

* [Hessian](http://hessian.caucho.com/doc/hessian-serialization.html)

* [ZeroC ICE](https://doc.zeroc.com/ice/3.7/ice-protocol-and-encoding)

### …​ Cap’N Proto, FlatBuffers? ###

Most of the arguments from the previous answer (for Google Protocol
Buffers, ASN.1, Apache Thrift, Apache Avro, BSON) apply here as
well. Both Cap’N Proto and FlatBuffers are not a tool for reading or
writing arbitrary formats. Instead, they uses a couple of clever
tricks to make serialization and deserialization more efficient
(casting binary structures as blocks, not assigning individual
fields), but, essentially, they emphasize content, and offer very
limited control over serialization format.

In theory, [Cap’N Proto encoding scheme](https://capnproto.org/encoding.html) is well documented and
can be implemented in .ksy to parse Cap’N Proto encoded messages.

Software mentioned

* [Cap’N Proto](https://capnproto.org/)

* [FlatBuffers](https://google.github.io/flatbuffers/)

### …​ GNU Bison, Yacc, Lex, Flex, ANTLR, etc? ###

All these tools actually work on parsing text (most usually, source code)
using context-free grammars. The core problem they solve is ambiguity of
whatever was read. For example, a single letter `a` might be part of
string literal, part of an identifier, part of a tag name, etc. In most
cases, parsers that they generate have a concept of **state** and a fairly
complex ruleset to change states. On the other hand, binary files are
usually structured in a non-ambiguous way: there’s no need to do complex
backtracking, re-interpreting everything in a different fashion just
because we’ve encountered something near the end of the file. There’s
usually no **state** beyond the pointer in the stream and pointer the code
that does parsing.

Software mentioned

* [GNU Bison](https://www.gnu.org/software/bison/)

* [Yacc](https://en.wikipedia.org/wiki/Yacc)

* [Lex](https://en.wikipedia.org/wiki/Lex_(software))

* [Flex](https://github.com/westes/flex)

* [ANTLR](https://www.antlr.org/)

### …​ SweetScape 010 Editor, Synalysis, Hexinator, Okteta, iBored? ###

All these tools are advanced hex editors with some sort of **template
language**, which is actually pretty close to `.ksy` language. One major
difference is that `.ksy` files, unlike per-editor templates, can be
compiled right into parser source code in any supported language.

Software mentioned

* [SweetScape 010 Editor](https://www.sweetscape.com/010editor/)

* [Synalysis](https://www.synalysis.net/)

* [Hexinator](https://hexinator.com/)

* [Okteta](https://docs.kde.org/trunk5/en/extragear-utils/okteta/tools-structures.html)

* [iBored](http://apps.tempel.org/iBored/)

### …​ Preon? ###

* Both Preon and KS are declarative

* Preon is Java-only library, KS is a cross-language tool

* Preon’s data structure definitions are done as annotations inside `.java` source files, KS keeps structure definitions in separate `.ksy` file

* Preon interprets data structure annotations in runtime, KS compiles `.ksy` into regular `.java` files first, then they’re compiled normally by Java compiler as part of the project

* Preon supports unaligned bit streams, KS does not (yet)

Software mentioned

* [Preon](https://github.com/preon/preon)

Format specification: how to …​
----------

### …​ use variable-length integer quantities (AKA VLQ, varint, vint, LEB128/ULEB128, 7-bit encoded int, Base-128 encoding)? ###

In most cases, you can just import existing implementation from our
stdlib:

* [vlq\_base128\_be](//formats.kaitai.io/vlq_base128_be/) for
  big-endian VLQ (as used in ASN.1 BER encoding, standard MIDI file
  format, etc)

* [vlq\_base128\_le](//formats.kaitai.io/vlq_base128_le/) for
  little-endian VLQ (as used in DWARF debugging info, Google Protocol
  Buffers, Apache Lucene, Apache Avro, etc)

Typical usage example:

```
meta:
  id: test_vlq
  imports:
    - /common/vlq_base128_le
seq:
  - id: len
    type: vlq_base128_le
  - id: buf
    size: len.value
```

### …​ binary-coded decimals (BCD)? ###

There’s lot of variety when it comes to BCD representations:

* Number of decimal digits is different

* BCDs that use byte per digit or nibble (half-of-a-byte) per digit

* Endianness: might be little or big

Kaitai Struct stdlibs include a parameterized type[bcd](//formats.kaitai.io/bcd/) which supports majority of these BCD
versions using parameters (available in Kaitai Struct v0.8+):

* `num_digits` — integer, number of digits (valid values: 1..8)

* `bits_per_digit` — integer, number of bits per digit (valid values: 4 or 8)

* `is_le` — boolean, specifies order of digits: true if little-endian,
  false if big-endian

Typical usage example:

```
meta:
  id: test_bcd
  imports:
    - /common/bcd
seq:
  - id: len                # In stream: 03 02 01 00 00
    type: bcd(5, 8, true)
  - id: buf                # Buffer of 123 bytes
    size: len.as_int
```

Note

 If you don’t need to access BCD value as an integer or a string
(for example, it is very often used to store serial numbers and
identifiers in hardware protocols), consider just treating it as an
opaque byte array.
