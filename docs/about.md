---
layout: page
---

RVT is a collection of tools/libraries to support both static
and dynamic verification of Rust programs.

We see static verification (formal verification) and dynamic verification
(testing) as two parts of the same activity and so these tools can be used for
either form of verification.

- Dynamic verification using the
  [proptest](https://github.com/AltSysrq/proptest)
  fuzzing/property testing library.

- Static verification using the
  [KLEE](http://klee.github.io/)
  symbolic execution engine.

We aim to add other backends in the near future.

In addition, [we document]({{ site.baseurl }}{% link Documentation.md %}) how the tools we wrote work
in case you are porting a verification tool for use with Rust.
(In particular, we describe how to generate LLVM bitcode files that can
be used with LLVM-based verification tools.)


## Usage

TL;DR

1. Install the dockerfile [instructions]({{ site.baseurl }}{% link installation.md %}).

    ``` shell
    git clone https://github.com/project-oak/rust-verification-tools.git
    cd rust-verification-tools
    docker/build
    ```

2. Fuzz some examples with proptest

   ```
   cd compatibility-test
   cargo test
   cd ..
   ```

   (You can also use
   `cargo-verify --backend=proptest --verbose compatibility-test`.)

   One test should fail – this is correct behaviour.

3. Verify some examples with propverify

   `cargo-verify --tests verification-annotations`

   `cargo-verify --tests compatibility-test`

   No tests should fail.

4. Read [the propverify intro]({{ site.baseurl }}{% link using-propverify.md %}) for an example
   of fuzzing with `proptest` and verifying with `propverify`.

5. Read [the proptest book](https://altsysrq.github.io/proptest-book/intro.html)

6. Read the source code for the [compatibility test suite][compatibility-test].

   (Many of these examples are taken from or based on examples in
   [the proptest book](https://altsysrq.github.io/proptest-book/intro.html).)

There is also [some limited documentation]({{ site.baseurl }}{% link Documentation.md %}) of how this works.


## Installation

Follow the [installation instructions]({{site.baseurl}}{% link installation.md %}).


## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE][LICENSE-APACHE] or
  http://www.apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT][LICENSE-MIT] or
  http://opensource.org/licenses/MIT)

at your option.


## Acknowledgements

The `propverify` crate is heavily based on the design and API of the wonderful
[proptest](https://github.com/AltSysrq/proptest)
property/fuzz-testing library.
The implementation also borrows techniques, tricks and code
from the implementation – you can learn a lot about how to write
an embedded DSL from reading the proptest code.

In turn, `proptest` was influenced by
the [Rust port of QuickCheck](https://github.com/burntsushi/quickcheck)
and
the [Hypothesis](https://hypothesis.works/) fuzzing/property testing library for Python.
(`proptest` also acknowledges `regex_generate` – but we have not yet implemented
regex strategies for this library.)


## Known limitations

This is not an officially supported Google product;
this is an early release of a research project
to enable experiments, feedback and contributions.
It is probably not useful to use on real projects at this stage
and it may change significantly in the future.

Our current goal is to make `propverify` as compatible with
`proptest` as possible but we are not there yet.
The most obvious features that are not even implemented are
support for
using regular expressions for string strategies,
the `Arbitrary` trait,
`proptest-derive`.

We would like the `propverify` library and the `cargo-verify` script
to work with as many Rust verification tools as possible
and we welcome pull requests to add support.
We expect that this will require design/interface changes.


### Contribution

Unless you explicitly state otherwise, any contribution intentionally
submitted for inclusion in the
work by you, as defined in the Apache-2.0 license, shall be dual licensed as
above, without any
additional terms or conditions.

See [the contribution instructions][CONTRIBUTING] for further details.

[git repo]: https://github.com/project-oak/rust-verification-tools/
[LICENSE-APACHE]: https://github.com/project-oak/rust-verification-tools/blob/main/LICENSE-APACHE
[LICENSE-MIT]: https://github.com/project-oak/rust-verification-tools/blob/main/LICENSE-MIT
[CONTRIBUTING]: https://github.com/project-oak/rust-verification-tools/blob/main/CONTRIBUTING.md
[compatibility-test]: https://github.com/project-oak/rust-verification-tools/blob/main/compatibility-test/src