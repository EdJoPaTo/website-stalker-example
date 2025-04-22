Kaitai Struct developer intro
==========

Kaitai Project
version 0.8

This document provides an overview of Kaitai Struct project from a
developer’s perspective: general architecture, infrastructure, etc.

1. Compiler’s architecture
----------

The heart of Kaitai Struct project is obviously[a reference compiler](https://github.com/kaitai-io/kaitai_struct_compiler).
As all compilers, it "compiles" or "translates" input files (Kaitai
Struct YAML, .ksy) into output files (source code in target
programming languages, like C++, Java, etc).

In order to do this translation, compiler performs several major
steps:

1. Loading of YAML files and parsing them into in-memory tree of
   objects

2. "Pre-compilation" - a set of preparatory actions (such as type
   inferring, resolving names, compile-time sanity checks), which are
   the same for all target languages

3. "Compilation" - traversal of the KSY object tree in certain order,
   rendering source code in target language by application of certain
   "templates"

2. Entry point
----------

Before these 3 keys steps are performed, there is always some entry
point to get us started. There are multiple, platform-dependent entry
points in the compiler:

* JVM: io.kaitai.struct.JavaMain does:

  * command-line argument parsing, which results in a `CLIConfig` object

  * runs JavaMain.run with it

  * runs JavaMain.compileOneInput for every .ksy source file specified,
    doing lots of wrapping to properly handle regular output and
    exceptions

* JS: io.kaitai.struct.MainJs has the main `compile` method

3. 3-step compilation process
----------

Current implementation bundles steps 1 and 2 into one invocation:

* For JVM, it is implemented in `JavaKSYParser.localFileToSpecs`

* For JS, it is implemented in `JavaScriptKSYParser.yamlToSpecs` -
  although note that whole JS is heavily async, so it returns`Future[ClassSpecs]`, not `ClassSpecs` object itself.

### 3.1. Loading and parsing of YAML files ###

The aim of this stage is, given a list of file names to load
(typically, these would be .ksy files) to load them, parse them as
YAML, and convert them to all into elements of`io.kaitai.struct.format` - typically various `*Spec` things, like`ClassSpec`, `AttributeSpec`, etc. End result is a single `ClassSpecs`object, which incorporates one or many `ClassSpec` which define user
types.

#### 3.1.1. Loading YAML files ####

Loading YAML files is currently, unfortunately, done by external
library in platform-specific manner:

* For JVM, it calls[SnakeYAML](https://bitbucket.org/snakeyaml/snakeyaml). Everything
  related to this step is encapsulated in `JavaKSYParser`.

* For JS, it calls: TODO

We’re working on bringing pure Scala YAML parser, but it’s a
relatively distant goal: see[#229](https://github.com/kaitai-io/kaitai_struct/issues/229).

#### 3.1.2. Parsing ####

Conversion from YAML objects to Spec-objects is typically performed by
invocation of `ClassSpec.fromYaml`.

#### 3.1.3. Loading imports ####

After we’ve parsed YAML, we can recursively load all files mentioned
in imports. The biggest catch in this process is that it is
effectively reading more disk files + running more YAML parsing,
i.e. it’s a step back, again into platform-dependent
territory.

### 3.2. Precompilation ###

The aim of this stage is to do preparatory language-independent
actions. The whole step is invoked from `Main.precompile`, but
individual substeps are implemented by classes in`io.kaitai.struct.precompile`. Please refer to per-class documentation
(if it exists) to every particular step.

Precompilation modifies (enriches) existing ClassSpecs
object. Alternatively, it might throw an exception if some of the
validation checks failed (TODO: exception structure).

### 3.3. Compilation ###

Compilation is a final step, which converts enriched ClassSpecs into
source code in target language.

This task is obviously dependent on target language, thus it is
performed by language-specific class.

There are 2 main variations of implementing these:

* Classes which inherit `AbstractCompiler` directly, such as`GraphVizCompiler`, do everything from scratch and organize
  generation flow in some arbitrary manner.

* Most traditional languages (such as Java, Ruby, Python, C++, etc),
  which has something in common, use ready-made `ClassCompiler`, which
  is a simple skeleton for compiling something resembling typical
  understanding of a "class" with members/methods. To introduce
  language-specific behavior, one can:

  * Provide implementation of `LanguageCompiler`, which is acts like a
    template with many different simple methods like "start new file",
    "start new class", "finish a class", etc.

  * Subclass `ClassCompiler` (like `GoClassCompiler`), overriding some
    of the control flow.

#### 3.3.1. Translators ####

During compilation process, we occasionally need to do translation of
KS expression language (which is target language-agnostic) into actual
target language snippets. "Translators" are per-language classes
reside in `io.kaitai.struct.translators` which implement that
translation. The most important method they provide is `translate`,
which gets KS expression and is expected to return a string in target
language.

TODO: explain about translators which do not generated only a string
(i.e. Go).
