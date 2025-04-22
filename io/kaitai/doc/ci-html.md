Continuous Integration infrastructure
==========

Kaitai Project

Kaitai Struct project sports a relatively complex CI (Continuous
Integration) pipeline. This document describes how it’s working.

High-level overview
----------

Kaitai Struct CI strives to be highly modular and, by design, tries
not to rely on a single CI engine provider. Currently, we use:

* [Travis](https://app.travis-ci.com/github/kaitai-io)

* AppVeyor: [for kaitai\_struct](https://ci.appveyor.com/project/kaitai-io/kaitai-struct), [for ci\_targets](https://ci.appveyor.com/project/kaitai-io/ci-targets)

* GitHub Actions: [for kaitai\_struct\_formats](https://github.com/kaitai-io/kaitai_struct_formats/actions)

With so many different jobs/flows, it’s hard to rely on CI providers
internal tools (such as job browsers, test browsers, log explorers,
etc), so we’re using our own [CI dashboard](//ci.kaitai.io/) to
unify all the data coming from different test runs/sources and monitor
current status of the compiler.

The following (clickable) chart gives an overview of CI
pipeline, tracing the path for one particular target language (Ruby):

Kaitai Struct CI high-level overview

Figure 1: Kaitai Struct CI high-level overview

On a high level, it can be summarized as:

* We build the compiler: sources are in[compiler repo](https://github.com/kaitai-io/kaitai_struct_compiler),
  all dependencies are fetched automatically by build tooling (sbt).

* This results in several packages, which get published as artifacts
  to several artifact stores (our "unstable builds"). Some of these
  unstable builds trigger other products' pipelines (such as[Web IDE](https://ide.kaitai.io/)).

* We run internal compiler unit tests (`test_compiler`).

* We fetch test .ksy files from[tests repo](https://github.com/kaitai-io/kaitai_struct_tests) (\~150
  tests), and run compiler on them, asking for every possible target
  language.

* This produces \~150 tests × \~15 targets \~ 1500 compiled format files
  in various target languages. We push them all into[ci\_targets repo](https://github.com/kaitai-io/ci_targets) at GitHub.

* Once `ci_targets` is updated, this triggers lots of CI jobs in
  various environments in parallel. Every such job tests one
  particular target language in one particular environment. To
  identify them, we give every such job a name in form of`language/environment`. For example:

  * `ruby/1.9` tests "ruby" target language in default (Linux)
    environment, using Ruby 1.9 (at Travis).

  * `cpp_stl_11/msvc141_windows_x64` tests "cpp\_stl\_11" (which is
    actually a subvariant of "cpp\_stl" target with compiler options set
    to generate exactly C11 code using STL library), building and
    running it in Windows environment with Microsoft Visual C
    compiler, toolkit version 141, x64 architecture. This job runs in
    AppVeyor CI.

* Every test job eventually produces test results, which get pushed
  into [ci\_artifacts repo](https://github.com/kaitai-io/ci_artifacts/). Every job gets individual branch: for example,[ruby/1.9 branch](https://github.com/kaitai-io/ci_artifacts/tree/ruby/1.9) keeps results of `ruby/1.9` test run.

* Finally, these test results can be viewed online at our[CI dashboard](//ci.kaitai.io/), which is a simple JavaScript
  app which fetches and aggregates all test results from all runs on
  the fly.

Main CI pipeline in details
----------

### Compiler ###

Compiler is the heart of everything in Kaitai Struct, so it’s only
natural that we focus on making compiler maintenance as automated as
possible.

* Everything starts with[compiler](https://github.com/kaitai-io/kaitai_struct_compiler) repo.

* A new commit (or build request) for compiler repo triggers building
  of new compiler binaries. There are two builds running:

  * [compiler build at Travis](https://app.travis-ci.com/github/kaitai-io/kaitai_struct) runs on Linux and gets us .deb, .zip and .js builds of
    compiler

  * [compiler build at AppVeyor](https://ci.appveyor.com/project/kaitai-io/kaitai-struct) runs on Windows and gets us .msi Windows
    installer build of compiler

* These build results are already useful (as unstable builds for other
  projects / people who would like to test bleeding edge features) and
  they get published as artifacts:

  * Universal .zip packages get published in[universal\_unstable folder](https://bintray.com/kaitai-io/universal_unstable/kaitai-struct-compiler), powered by Bintray

  * Linux .deb packages get published in[debian\_unstable repo](https://bintray.com/kaitai-io/debian_unstable/kaitai-struct-compiler), powered by Bintray

  * Windows .msi packages become available at[AppVeyor project build artifacts](https://ci.appveyor.com/project/kaitai-io/kaitai-struct/build/artifacts)

  * JavaScript compiler build gets packaged as npm module and published
    as[kaitai-struct-compiler npm package](https://www.npmjs.com/package/kaitai-struct-compiler)

Note

 Direct links / instructions how to reach these downloads are
available as "unstable" at [Kaitai homepage / Download](//kaitai.io/)

* After compiler builds are finished, we run the internal compiler
  unit tests (`test_compiler`). These are[included inside compiler repo](https://github.com/kaitai-io/kaitai_struct_compiler/tree/master/jvm/src/test/scala/io/kaitai/struct) and are supposed to test individual functions
  & methods inside the compiler.

### Building tests formats ###

After we’ve got the compiler, next steps is to take "test formats" (a
large bunch of different input .ksy files) and run compiler on
them. `build_formats` process does that. To do that, we’ll need:

* Obviously, pre-built kaitai-struct-compiler

* Test format files (.ksy), which will come from[formats/ dir in tests repo](https://github.com/kaitai-io/kaitai_struct_tests/tree/master/formats)

This results in many files in target languages generated in`compiled/$LANG` directories. That directory gets pushed into[ci\_targets repo](https://github.com/kaitai-io/ci_targets). One can use
version control history in that repo to track which formats code
generation has changed over development iterations.

### Running test formats ###

The exact mechanism of "building and running tests" largely depends
on target language and environment, but there are a few common
things:

* The scripts to automate it come from[tests repo](https://github.com/kaitai-io/kaitai_struct_tests) again.

* All these runs require some[binary inputs that they will parse](https://github.com/kaitai-io/kaitai_struct_tests/tree/master/src) — these also come from same tests repo.

* All languages require its relevant KS runtime to build & run. For
  example, for Ruby, we’ll fetch[ruby\_runtime repo](https://github.com/kaitai-io/kaitai_struct_ruby_runtime) at this stage.

Other CI pipelines
----------

### Web IDE ###

TODO

### Formats gallery ###

[Formats gallery](//formats.kaitai.io/) is a static website, which
provides user-friendly rendition of contents of our[formats repo](https://github.com/kaitai-io/kaitai_struct_formats/).

Its pipeline is very simple and consists of[only one job, running on GitHub Actions](https://github.com/kaitai-io/kaitai_struct_formats/actions):

* It fetches latest **stable** KS compiler from[our own repository at bintray](https://bintray.com/kaitai-io/debian/kaitai-struct-compiler).

* Then it uses it and[some script magic](https://github.com/kaitai-io/kaitai_struct_formats/tree/master/_build) to build compiled versions of these formats and,
  ultimately, static website.

* Static website gets published into[formats-kaitai-io.github.io repo](https://github.com/kaitai-io/formats-kaitai-io.github.io), which is served over HTTP to everyone as [http://formats.kaitai.io/](//formats.kaitai.io/)

### Documentation ###

TODO
