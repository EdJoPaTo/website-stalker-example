Adding support for new target language
==========

A general overview of what is needed to add support for new target language in reference KS compiler.

1. Get acquainted with KS as a user at least on the intermediate level
----------

Things to check out and familiarize oneself with:

* general .ksy structure, metadata

* sequences and instances

* primitive types

* repetitions

* user-defined types

* enums

* processing algorithms

Clone [central KS repo](https://github.com/kaitai-io/kaitai_struct/), learn [how to build a compiler from sources](developers.html), install prerequisites, try to build the compiler and run the tests. Take a look at our [CI](//ci.kaitai.io/).

2. Plan how to map KS concept to concepts of new target language
----------

The best way to get some inspiration in how it’s done is probably take one or two of existing target languages and experiment a little, seeing which KS concepts result in what generated code.

### 2.1. Structures ###

The core element that KS deals with is a "type". Basically, everything starts with a "type", i.e. a "file" is a "type". "Type" can include:

* a collection of fields parsed sequentially (`seq`)

* a number of fields parsed randomly or calculated (`instances`)

* definition of nested types (`types`)

* lists of integer constants (`enums`)

Most usually, a concept of "type" maps to a concept of "class" or "object" in target language, but it can be a standalone data structure with a couple of generated methods to work with it, or probably something completely different.

### 2.2. Streams ###

Struct has to parse the data from somewhere. Decide on which target language’s abstraction of stream is best (probably it’s good to support reading both from disk files, if they’re available, and from arbitrary byte buffers). One would probably need to implement a KaitaiStream-style wrapper for these stream(s), as it might lack some useful functions, like bit-level reading, read-until-the-terminator, etc.

### 2.3. Primitive and complex type mapping ###

KS deals with a few primitive and complex types:

* integer numbers

* floating point numbers

* byte arrays

* strings

* "generic" arrays of everything

Decide upon mapping of all these types into native types of target language. Pay extra attention to:

* signed vs unsigned support

* if target language has any platform-dependent types

* encoding support for strings

* substitutions / workarounds for everything that target language does not support

* nulls / undefined state of variables - these could be particularly useful to implement lazy instances parsing; if a language does not support such state of variables, we’ll have to introduce extra "flag" variables to store information

### 2.4. Coding standards, naming practices and other traditions in target language ###

Carefully check out different coding practices related to target language. If there is an official or semi-official standard or recommendation, try to follow it. Things to pay particular attention to:

* naming standards (i.e. UpperCamelCase, lowerCamelCase, under\_score\_case, something else) for various parts of generated code (names of source files, classes, methods, properties, etc)

* code formatting style and guidelines (indent size & practices)

* docstrings layout and general documentation standards

* private/protected/public access restriction traditions

3. Implement runtime library
----------

Keeping it close to [our standard API](stream_api.html) is heavily recommended, unless there’s some good reason to do it differently. In particular, try to stick to proposed method names, it will make life much easier.

4. Manually compile `hello_world.ksy`
----------

Take one simplest test [hello\_world.ksy](https://github.com/kaitai-io/kaitai_struct_tests/blob/master/formats/hello_world.ksy) and translate it manually into source code in a new target language, as it would have been compiled by KS compiler. Inspiration can be drawn from any other already supported language.

5. Start testing
----------

Choose a testing framework that target language would use. Ideally, we should be able to run it with installing little extra dependencies in our Travis CI configuration. At the bare minimum, we’ll need a command-line based test runner that will output some report file we can aggregate in our CI later (JUnit XML reports are usually good candidates).

Create testing infrastructure in [tests](https://github.com/kaitai-io/kaitai_struct_tests) repo: usually it boils down to:

* `spec/$LANG` - a project or just a bunch of files with test specs; it’s heavily recommended to do 1 test .ksy format = 1 test case = 1 file, if possible

* `run-$LANG` - a single script to launch test runner with all the tests

6. Port spec for HelloWorld
----------

Port spec for HelloWorld test to new target language and make it work with manually compiled `hello_world.ksy`.
