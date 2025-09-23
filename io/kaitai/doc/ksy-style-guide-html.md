KSY Style Guide
==========

Kaitai Project
version 0.11

Although .ksy files are treated as YAML files, and YAML syntax allows
quite a few representations of the same content, it is recommended to
maintain a certain style in .ksy files to aid collaboration. This
document serves as official .ksy style guide. In particular, we strive
to make sure that all formats in our[formats repository](https://github.com/kaitai-io/kaitai_struct_formats)are using this style.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
"SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this
document are to be interpreted as described in[RFC 2119](https://tools.ietf.org/html/rfc2119).

This document is work in progress, not all sections are complete yet.

1. General formatting
----------

MUST use:

* Single implicit YAML document per file (i.e. no `---` header).

* No `%YAML x.y` version directives, no `%TAG` directives.

* 2-space indent.

* UTF-8 encoding throughout the file.

* LF (AKA "UNIX") line endings.

* Trailing newline character in a .ksy file.

* Block YAML style in most general cases, unless explicitly
  specified/allowed otherwise.

Formatting of sequences MUST include an indent, i.e.:

Good

```
imports:
  - foo
  - bar
```

Bad

```
imports:
- foo
- bar
```

Formatting of maps-inside-sequences MUST have `-` delimiter and first
map element on the same first line, i.e.:

Good

```
- id: foo
  type: u1
- id: bar
  type: u2
  enum: baz
```

Bad

```
-
  id: foo
  type: u1
-
  id: bar
  type: u2
  enum: baz
```

All identifiers, docstrings, comments and generally all human-readable
text SHOULD be kept in English, unless there’s a very good reason not
to do so.

2. Order of sections in a type spec
----------

Use the following order of sections:

1. `meta`, if present, MUST go first

2. `doc`

3. `doc-ref`

4. `to-string`

5. `params`

6. `seq`

7. `instances`

8. `types`, `enums` — use one’s best judgement to order these two to
   maximize readability

3. Meta section (`meta`)
----------

Meta section is mostly used to specify additional ("meta") information
for a particular file format, so 99% of time it is only present for
top-level type. In some cases, meta section might be specified in
intermediate types as well, for example, to switch default endianness
or encoding. Thus, style recommendations for "top-level" meta sections
and "intermediate" meta sections are different, as they serve slightly
different purposes.

For top-level meta section, use the following order of keys:

1. `id` — main identifier, MUST match the name of the `.ksy` file

2. Human-readable meta-information (in order of importance, at least
   one MUST be present):

   1. `title`

   2. `application` — SHOULD name a particular application, if there’s
      any; if there are too many to list (for example, network packet
      formats or executables are used virtually everywhere), then one
      SHOULD omit this field.

   3. `file-extension` — if there’s only one extension, MUST be a
      string; if there are several, MUST be an sequence in block form
      and SHOULD order extensions from most popular extension to least
      popular.

   4. `xref` — keys inside MUST be in alphabetic order

   5. `tags` — values inside MUST be in alphabetic order

3. Legal information — `license` — MUST be a valid[SPDX license expression](https://spdx.org/licenses/)

4. Processing instructions:

   1. `ks-version` — SHOULD list lowest possible KS compiler version that
      is able to compile this file.

   2. `imports`

5. Defaults (in alphabetic order):

   1. `encoding`

   2. `endian`

   3. `bit-endian`

For intermediate-level meta sections, use the following order of keys:

1. Defaults (in alphabetic order):

   1. `encoding`

   2. `endian`

   3. `bit-endian`

Note

 KS syntax allows usage of some top-level elements deep inside
the hierarchy — this can be useful during development, for example,
for purpose of grafting one .ksy file into another quickly. However,
in production-quality .ksy files, one MUST NOT use keys like `title`,`imports` or `ks-version` (i.e. everything except explicitly listed in
a list above) on intermediate levels.

The following keys are reserved for internal use (i.e. debugging and
test running) and MUST NOT be used in general-purpose .ksy files:

* `ks-debug`

* `ks-opaque-types`

4. Documentation
----------

### 4.1. `doc` ###

Formatting:

* Single-line documentation strings SHOULD BE formatted using raw
  unquoted string literals.

* Multi-line SHOULD BE formatted using[YAML literal style scalar](https://yaml.org/spec/1.2/spec.html#id2795688), i.e. using `: |` syntax. An example:

```
doc: |
  File index entry contains intricate details about file in the
  archive: there are both meta-information attributes (such as file
  names, locations, various timestamps, etc) and references to
  inodes, which can be used to find file body in the container.

  For networked locations, file index entry uses an optional
  `remote_resource` type. Proper usage sequence is:

  * check `code` to be one that requires network usage
  * determine file name using `name_networked` instance and check if
    it's really a file requested by the user
  * proceed to query information from networked resource given by
    `resource` attribute
```

Lines should be wrapped to be 80 columns long. If it doesn’t fit into
single line after wrapping, then it’s a multi-line docstring, so use
proper multi-line syntax.

There is no formal conversion of docstrings into language-specific
docstrings now in KS, but generally we SHOULD keep it close to[CommonMark formatting](https://commonmark.org/), i.e.:

* paragraphs separated by an empty line

* bullet lists created by an asterisk `*` and a space at the beginning
  of the line

* use backticks ``` to wrap identifiers and small pieces of
  code

TODO: documentation contents, what should and should no be included

### 4.2. `doc-ref` ###

TODO

5. Sequence attributes
----------

When specifying an attribute, one MUST use the following order of keys:

1. Identifier(s)

   1. `id`

   2. `-orig-id` — use to specify original ID spelling if transcribing a
      structure from existing software and/or official spec

2. `size`

3. `size-eos`

4. `type`

5. Type-related keys:

   1. `enum`

   2. `terminator`

   3. `include`

   4. `consume`

   5. `eos-error`

   6. `pad-right`

   7. `encoding`

6. `process`

7. `valid`, `contents`

8. Repetition-related keys:

   1. `repeat`

   2. `repeat-expr`, `repeat-until`

9. `if`

10. `doc`

11. `doc-ref`

Every key is optional. Attributes SHOULD have at least `id` and `doc`— however, see below for notes about omitting `id`, and `doc` SHOULD
NOT be included if it’s trivial (i.e. if it is a copy of `id`, and
there is really nothing more to say about that attribute).

### 5.1. Attribute identifiers (`id`) ###

KS enforces specific identifier style in the language -`lower_underscore_case` (it is needed to be able to convert to other
styles of identifier spelling, like `UpperCamelCase` or`lowerCamelCase`, which some target languages use).

KS allows omitting `id`. One MUST omit `id` to mark up attributes of
unknown/undetermined purpose, i.e. unfinished reverse engineering
work. One MUST NOT omit `id` to mark up reserved/unused attributes and
padding, i.e. placeholder that are known to be empty and unused.

One SHOULD use the following rules to maintain consistency across
various KSY files. Doing that would maintain the "principle of least
surprise" and make life easier to end-users, reducing amount of
guesswork.

* For simple non-repeated fields, use a simple singular form —
  e.g. `width`, `header`, `transaction_id`, `file`.

* For an array of objects (i.e. with `repeat: something`), use plural
  form — e.g. `files`, `transactions`.

* Don’t be overly verbose: use commonly understood abbreviations
  liberally, if it will improve readability — e.g. `src_mac` or`src_mac_addr` instead of `source_media_access_control_address`

* For fields that are designed to be used to detect file type (AKA
  "magic values"), use `magic` name, or, if there are several of them,`magic1`, `magic2`, etc.

* For reserved fields which are **known** to be unused, use `reserved`name (or `reserved1`, `reserved2`, etc, if there are many of them)

* For fields that designate **number / count** of something (in
  particular, number of repetitions of some other structure), use`num_` prefix and plural form — i.e. `num_questions`, `num_blocks`,`num_nodes`

* For fields that designate **offset** to some particular data structure,
  use `ofs_` prefix and name of that data structure (as it would appear
  in the file) — i.e. `ofs_block`, `ofs_queries`, `ofs_path`

* For fields that designate **size** of some particular data structure
  (in bytes or some other fixed units), use `len_` prefix and name of
  that data structure — i.e. `len_block` (length of a single `block`entry), `len_blocks` (total length of whole `blocks` array, made of`block` entries).

Note

 See [Transcribing existing specs](#transcribing) for more info on preserving / renaming
identifiers when transcribing existing spec into KSY.

### 5.2. Trailing padding ###

If you’re using a size-limited substream for a structure, one MUST NOT
specify manually calculated or auto-calculated extra padding to make
structure consume whole substream. Just omit it — it will save memory
and CPU time on parsing.

Good

```
seq:
  - id: header
    size: 64
    type: block
types:
  block:
    seq:
      - id: param1
        type: u4
      - id: param2
        type: u2
```

Bad

```
seq:
  - id: header
    size: 64
    type: block
types:
  block:
    seq:
      - id: param1
        type: u4
      - id: param2
        type: u2
      - id: padding
        size-eos: true
```

Worst

```
seq:
  - id: header
    size: 64
    type: block
types:
  block:
    seq:
      - id: param1
        type: u4
      - id: param2
        type: u2
      - id: padding
        size: 58
        # 64 - 4 - 2
```

6. Instance attributes
----------

Instance attribute use the superset of keys which are allowed in
sequence attributes (except for `id`), thus all ordering rules apply
here as well. Keys MUST appear in this order:

1. `-orig-id` (optional)

2. `io` (optional)

3. `pos` or `value`

4. All other keys (except for `id` and `-orig-id`), in order specified
   in [Sequence attributes](#seq-attr)

7. Transcribing existing specs
----------

When transcribing structures already described in some other existing
spec or software, note that it’s not necessary to copy existing
identifiers to `id` keys (in verbatim or modified form) or even
maintain same structures as types.

The rationale of doing so is that a lot of existing specs rely on
particular standards and approaches of some target language and/or
platform. Sometimes, existing specs are burdened by some legacy
(i.e. they are obliged to maintain names of fields, even when its true
purpose was extended since its introduction for compatibility with
older software). KS, on the other hand, is cross-platform and
cross-language, thus it is not necessary (and in many cases, it’s just
impossible) to stick to single platform’s style. And KS-provide API is
to be used by new software anyway, so you don’t usually need to be
concerned with legacy compatibility.

Use `-orig-id` key to specify original names of fields for purposes of
maintaining a reference link to parts of original spec, but,
otherwise, feel free to use a more consistent and language-neutral
approach in naming attributes and types.

### 7.1. Windows struct ###

For example, consider this[MMCKINFO Windows structure](https://docs.microsoft.com/en-us/windows/win32/api/mmiscapi/ns-mmiscapi-mmckinfo), as specified in MSDN:

```
typedef struct {
  FOURCC ckid;
  DWORD  cksize;
  FOURCC fccType;
  DWORD  dwDataOffset;
  DWORD  dwFlags;
} MMCKINFO;
```

It is pretty inconsistent:

* Some fields use abbreviated lower case (`ckid` — as it stands for
  "chunk ID"), others use upper camel case (`dwDataOffset`).

* Some fields use so-called "Hungarian notation", i.e. prepending type
  information before identifier (i.e. `fccType` = "type, four-CC",`dwDataOffset` = "data offset, double word"), some don’t (`ckid`,`cksize`).

* Some abbreviations are very brief (`ckid`), some are pretty verbose
  (`dwDataOffset`).

* Actually, `dwDataOffset` and `cksize` specify offset and size of the
  same data structure (called "chunk’s data member" in human-readable
  annotation).

Also, this definition does not specify flag values (i.e. in a C struct
union syntax), but instead relies of flag constant definitions
elsewhere, which is also pretty inconvenient.

Recommended way to lay out that structure in KS would be something like that:

```
seq:
  - id: chunk_id
    -orig-id: ckid
    type: u4
    enum: four_cc
  - id: len_data
    -orig-id: cksize
    type: u4
  - id: type
    -orig-id: fccType
    type: u4
    enum: four_cc
  - id: ofs_data
    -orig-id: dwDataOffset
    type: u4
  - id: flags
    -orig-id: dwFlags
    type: flags
    size: 4
instances:
  data:
    pos: ofs_data
    size: len_data
types:
  flags:
    # add a comprehensive type that describes flags here
```

Note that we’ve clearly separated names and types here, used standard`ofs_` and `len_` prefixes for referencing offset and length of a
particular structure (named "data", short for "chunk’s data member",
in this case). Also, we’ve added `data` instance to access that
structure directly.

### 7.2. Linux struct ###

Another example is ELF executable header, as specified in elf.h in
Linux:

```
typedef struct
{
  unsigned char e_ident[EI_NIDENT];     /* Magic number and other info */
  Elf32_Half    e_type;                 /* Object file type */
  Elf32_Half    e_machine;              /* Architecture */
  Elf32_Word    e_version;              /* Object file version */
  Elf32_Addr    e_entry;                /* Entry point virtual address */
  Elf32_Off     e_phoff;                /* Program header table file offset */
  Elf32_Off     e_shoff;                /* Section header table file offset */
  Elf32_Word    e_flags;                /* Processor-specific flags */
  Elf32_Half    e_ehsize;               /* ELF header size in bytes */
  Elf32_Half    e_phentsize;            /* Program header table entry size */
  Elf32_Half    e_phnum;                /* Program header table entry count */
  Elf32_Half    e_shentsize;            /* Section header table entry size */
  Elf32_Half    e_shnum;                /* Section header table entry count */
  Elf32_Half    e_shstrndx;             /* Section header string table index */
} Elf32_Ehdr;
```

This one is less inconsistent, but still could be improved:

* It uses its own convention for specifying "offset", "size" and
  "count" attributes.

* It prepends `e_` prefix to every element, which would serve
  absolutely no purpose in KS

* It uses its own non-standard system of types (`Elf32_Half`,`Elf32_Word`, `Elf32_Addr`, etc)

* `e_ident` actually is a complex 16-byte multi-member structure,
  which includes 4 bytes of magic number to identify a file format and
  12 bytes worth of extra fields

* Abbreviations are way too short (i.e. `ph` for "program header",`sh` for "section header", `eh` for "ELF header") for a casual user
  to understand its meaning without a documentation lookup. This can
  be easily remedied by using slightly more verbose names.

Thus, the recommended way to represent it would be:

```
seq:
  - id: magic
    -orig-id: e_ident
    contents:
      - 0x7f
      - "ELF"
    doc: Magic number
  # add extra members for these 12 bytes here
  - id: file_type
    -orig-id: e_type
    type: u2
    doc: Object file type
  - id: machine
    -orig-id: e_machine
    type: u2
    doc: Architecture
  # ...
  - id: ofs_program_headers
    -orig-id: e_phoff
    type: u4
    doc: Program header table file offset
  # ...
instances:
  program_headers:
    pos: ofs_program_headers
    repeat: expr
    repeat-expr: num_program_headers
    size: len_program_header
    type: program_header
```

### 7.3. C struct as "header" ###

Sometimes existing implementations use structures where they are
actually not necessary. This is, again, frequently done to satisfy
constraints of particular implementation, like C struct being of a
fixed size. KS does not have these restrictions, so in some cases one
can embed C struct "headers" right into the type and it would be
totally ok.

For example, consider the following description:

>
>
>
>
> Image file starts with a header, which consists of:
>
>
>
>
>
>
>
> * 4 bytes - magic number, must be 0x11335577
>
>
> * 4 bytes integer - width of image in pixels
>
>
> * 4 bytes integer - height of image in pixels
>
>
>
>
>
>
>
>
>
> Then raw image data follows, width \* height bytes.
>
>
>
>

Naive C implementation of this format would likely split this format
into a "header" structure and a "body", header being declared as:

```
typedef struct {
    uint32_t magic;
    uint32_t width;
    uint32_t height;
} image_header_t;
```

Straightforward conversion of that structures would result in:

```
seq:
  - id: header
    type: image_header
  - id: image_data
    size: header.width * header.height
types:
  image_header:
    seq:
      - id: magic
        contents: [0x11, 0x33, 0x55, 0x77]
      - id: width
        type: u4
      - id: height
        type: u4
```

However, in KS, this is very redundant and unnecessarily complex. One
can just put everything in one simple type — this is easier to read,
understand and use (and it does not make up artificial "header" entity
where we can avoid it):

```
seq:
  - id: magic
    contents: [0x11, 0x33, 0x55, 0x77]
  - id: width
    type: u4
  - id: height
    type: u4
  - id: image_data
    size: width * height
```
