[Lints](#lints)
==========

`rustdoc` provides lints to help you writing and testing your documentation. You
can use them like any other lints by doing this:

```
#![allow(unused)]
#![allow(rustdoc::broken_intra_doc_links)] // allows the lint, no diagnostics will be reported
#![warn(rustdoc::broken_intra_doc_links)] // warn if there are broken intra-doc links
#![deny(rustdoc::broken_intra_doc_links)] // error if there are broken intra-doc links
fn main() {
}
```

Note that, except for `missing_docs`, these lints are only available when running `rustdoc`, not `rustc`.

Here is the list of the lints provided by `rustdoc`:

[`broken_intra_doc_links`](#broken_intra_doc_links)
----------

This lint **warns by default**. This lint detects when an [intra-doc link](write-documentation/linking-to-items-by-name.html) fails to be resolved. For example:

```
#![allow(unused)]
fn main() {
/// I want to link to [`Nonexistent`] but it doesn't exist!
pub fn foo() {}
}
```

You'll get a warning saying:

```
warning: unresolved link to `Nonexistent`
 --> test.rs:1:24
  |
1 | /// I want to link to [`Nonexistent`] but it doesn't exist!
  |                        ^^^^^^^^^^^^^ no item named `Nonexistent` in `test`

```

It will also warn when there is an ambiguity and suggest how to disambiguate:

```
#![allow(unused)]
fn main() {
/// [`Foo`]
pub fn function() {}

pub enum Foo {}

pub fn Foo(){}
}
```

```
warning: `Foo` is both an enum and a function
 --> test.rs:1:6
  |
1 | /// [`Foo`]
  |      ^^^^^ ambiguous link
  |
  = note: `#[warn(rustdoc::broken_intra_doc_links)]` on by default
help: to link to the enum, prefix with the item type
  |
1 | /// [`enum@Foo`]
  |      ^^^^^^^^^^
help: to link to the function, add parentheses
  |
1 | /// [`Foo()`]
  |      ^^^^^^^

```

[`private_intra_doc_links`](#private_intra_doc_links)
----------

This lint **warns by default**. This lint detects when [intra-doc links](write-documentation/linking-to-items-by-name.html) from public to private items.
For example:

```
#![allow(unused)]
#![warn(rustdoc::private_intra_doc_links)] // note: unnecessary - warns by default.

fn main() {
/// [private]
pub fn public() {}
fn private() {}
}
```

This gives a warning that the link will be broken when it appears in your documentation:

```
warning: public documentation for `public` links to private item `private`
 --> priv.rs:1:6
  |
1 | /// [private]
  |      ^^^^^^^ this item is private
  |
  = note: `#[warn(rustdoc::private_intra_doc_links)]` on by default
  = note: this link will resolve properly if you pass `--document-private-items`

```

Note that this has different behavior depending on whether you pass `--document-private-items` or not!
If you document private items, then it will still generate a link, despite the warning:

```
warning: public documentation for `public` links to private item `private`
 --> priv.rs:1:6
  |
1 | /// [private]
  |      ^^^^^^^ this item is private
  |
  = note: `#[warn(rustdoc::private_intra_doc_links)]` on by default
  = note: this link resolves only because you passed `--document-private-items`, but will break without

```

[`missing_docs`](#missing_docs)
----------

This lint is **allowed by default**. It detects items missing documentation.
For example:

```
#![warn(missing_docs)]

pub fn undocumented() {}
fn main() {}
```

The `undocumented` function will then have the following warning:

```
warning: missing documentation for a function
  --> your-crate/lib.rs:3:1
   |
 3 | pub fn undocumented() {}
   | ^^^^^^^^^^^^^^^^^^^^^

```

Note that unlike other rustdoc lints, this lint is also available from `rustc` directly.

[`missing_crate_level_docs`](#missing_crate_level_docs)
----------

This lint is **allowed by default**. It detects if there is no documentation
at the crate root. For example:

```
#![allow(unused)]
#![warn(rustdoc::missing_crate_level_docs)]
fn main() {
}
```

This will generate the following warning:

```
warning: no documentation found for this crate's top-level module
  |
  = help: The following guide may be of use:
          https://doc.rust-lang.org/nightly/rustdoc/how-to-write-documentation.html

```

This is currently "allow" by default, but it is intended to make this a
warning in the future. This is intended as a means to introduce new users on*how* to document their crate by pointing them to some instructions on how to
get started, without providing overwhelming warnings like `missing_docs`might.

[`missing_doc_code_examples`](#missing_doc_code_examples)
----------

This lint is **allowed by default** and is **nightly-only**. It detects when a documentation block
is missing a code example. For example:

```
#![warn(rustdoc::missing_doc_code_examples)]

/// There is no code example!
pub fn no_code_example() {}
fn main() {}
```

The `no_code_example` function will then have the following warning:

```
warning: Missing code example in this documentation
  --> your-crate/lib.rs:3:1
   |
LL | /// There is no code example!
   | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

```

To fix the lint, you need to add a code example into the documentation block:

```
#![allow(unused)]
fn main() {
/// There is no code example!
///
/// ```
/// println!("calling no_code_example...");
/// no_code_example();
/// println!("we called no_code_example!");
/// ```
pub fn no_code_example() {}
}
```

[`private_doc_tests`](#private_doc_tests)
----------

This lint is **allowed by default**. It detects documentation tests when they
are on a private item. For example:

```
#![warn(rustdoc::private_doc_tests)]

mod foo {
    /// private doc test
    ///
    /// ```
    /// assert!(false);
    /// ```
    fn bar() {}
}
fn main() {}
```

Which will give:

```
warning: Documentation test in private item
  --> your-crate/lib.rs:4:1
   |
 4 | /     /// private doc test
 5 | |     ///
 6 | |     /// ```
 7 | |     /// assert!(false);
 8 | |     /// ```
   | |___________^

```

[`invalid_codeblock_attributes`](#invalid_codeblock_attributes)
----------

This lint **warns by default**. It detects code block attributes in
documentation examples that have potentially mis-typed values. For example:

```
#![allow(unused)]
#![warn(rustdoc::invalid_codeblock_attributes)]  // note: unnecessary - warns by default.

fn main() {
/// Example.
///
/// ```should-panic
/// assert_eq!(1, 2);
/// ```
pub fn foo() {}
}
```

Which will give:

```
warning: unknown attribute `should-panic`. Did you mean `should_panic`?
 --> src/lib.rs:1:1
  |
1 | / /// Example.
2 | | ///
3 | | /// ```should-panic
4 | | /// assert_eq!(1, 2);
5 | | /// ```
  | |_______^
  |
  = note: `#[warn(rustdoc::invalid_codeblock_attributes)]` on by default
  = help: the code block will either not be tested if not marked as a rust one or won't fail if it doesn't panic when running

```

In the example above, the correct form is `should_panic`. This helps detect
typo mistakes for some common attributes.

[`invalid_html_tags`](#invalid_html_tags)
----------

This lint **warns by default**. It detects unclosed
or invalid HTML tags. For example:

```
#![allow(unused)]
#![warn(rustdoc::invalid_html_tags)]

fn main() {
/// <h1>
/// </script>
pub fn foo() {}
}
```

Which will give:

```
warning: unopened HTML tag `script`
 --> foo.rs:1:1
  |
1 | / /// <h1>
2 | | /// </script>
  | |_____________^
  |
  note: the lint level is defined here
 --> foo.rs:1:9
  |
1 | #![warn(rustdoc::invalid_html_tags)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^

warning: unclosed HTML tag `h1`
 --> foo.rs:1:1
  |
1 | / /// <h1>
2 | | /// </script>
  | |_____________^

warning: 2 warnings emitted

```

[`invalid_rust_codeblocks`](#invalid_rust_codeblocks)
----------

This lint **warns by default**. It detects Rust code blocks in documentation
examples that are invalid (e.g. empty, not parsable as Rust). For example:

```
#![allow(unused)]
fn main() {
/// Empty code blocks (with and without the `rust` marker):
///
/// ```rust
/// ```
///
/// Invalid syntax in code blocks:
///
/// ```rust
/// '<
/// ```
pub fn foo() {}
}
```

Which will give:

```
warning: Rust code block is empty
 --> lint.rs:3:5
  |
3 |   /// ```rust
  |  _____^
4 | | /// ```
  | |_______^
  |
  = note: `#[warn(rustdoc::invalid_rust_codeblocks)]` on by default

warning: could not parse code block as Rust code
  --> lint.rs:8:5
   |
8  |   /// ```rust
   |  _____^
9  | | /// '<
10 | | /// ```
   | |_______^
   |
   = note: error from rustc: unterminated character literal

```

[`bare_urls`](#bare_urls)
----------

This lint is **warn-by-default**. It detects URLs which are not links.
For example:

```
#![allow(unused)]
#![warn(rustdoc::bare_urls)] // note: unnecessary - warns by default.

fn main() {
/// http://example.org
/// [http://example.net]
pub fn foo() {}
}
```

Which will give:

```
warning: this URL is not a hyperlink
 --> links.rs:1:5
  |
1 | /// http://example.org
  |     ^^^^^^^^^^^^^^^^^^ help: use an automatic link instead: `<http://example.org>`
  |
  = note: `#[warn(rustdoc::bare_urls)]` on by default

warning: this URL is not a hyperlink
 --> links.rs:3:6
  |
3 | /// [http://example.net]
  |      ^^^^^^^^^^^^^^^^^^ help: use an automatic link instead: `<http://example.net>`

warning: 2 warnings emitted

```

[`unescaped_backticks`](#unescaped_backticks)
----------

This lint is **allowed by default**. It detects backticks (`) that are not escaped.
This usually means broken inline code. For example:

```
#![allow(unused)]
#![warn(rustdoc::unescaped_backticks)]

fn main() {
/// `add(a, b) is the same as `add(b, a)`.
pub fn add(a: i32, b: i32) -> i32 { a + b }
}
```

Which will give:

```
warning: unescaped backtick
 --> src/lib.rs:3:41
  |
3 | /// `add(a, b) is the same as `add(b, a)`.
  |                                         ^
  |
note: the lint level is defined here
 --> src/lib.rs:1:9
  |
1 | #![warn(rustdoc::unescaped_backticks)]
  |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^
help: a previous inline code might be longer than expected
  |
3 | /// `add(a, b)` is the same as `add(b, a)`.
  |               +
help: if you meant to use a literal backtick, escape it
  |
3 | /// `add(a, b) is the same as `add(b, a)\`.
  |                                         +

warning: 1 warning emitted

```

[`redundant_explicit_links`](#redundant_explicit_links)
----------

This lint is **warn-by-default**. It detects explicit links that are the same
as computed automatic links.
This usually means the explicit links are removable. For example:

```
#![allow(unused)]
#![warn(rustdoc::redundant_explicit_links)] // note: unnecessary - warns by default.

fn main() {
/// add takes 2 [`usize`](usize) and performs addition
/// on them, then returns result.
pub fn add(left: usize, right: usize) -> usize {
    left + right
}
}
```

Which will give:

```
error: redundant explicit rustdoc link
  --> src/lib.rs:3:27
   |
3  | /// add takes 2 [`usize`](usize) and performs addition
   |                           ^^^^^
   |
   = note: Explicit link does not affect the original link
note: the lint level is defined here
  --> src/lib.rs:1:9
   |
1  | #![deny(rustdoc::redundant_explicit_links)]
   |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
   = help: Remove explicit link instead

```
