# `buck2-reference`

## Installing

Official install reference is [here](https://buck2.build/docs/about/getting_started/)

Typically it looks like this:

```bash
rustup install nightly-2024-06-08
cargo +nightly-2024-06-08 install --git https://github.com/facebook/buck2.git buck2
```

### Prelude

To clear the prelude:
```
git rm -f prelude
git rm --cached prelude
rm -rf .git/modules/prelude
# also check that it is not mentioned in .gitmodules
```

To install the prelude:

```bash
git submodule add https://github.com/facebook/buck2-prelude.git prelude
```

## Rules

Rules user docs are [here](https://buck2.build/docs/prelude/globals/)

Build rule concept overview is [here](https://buck2.build/docs/concepts/build_rule/)

Cheat sheet (less cool than this one) is [here](https://buck2.build/docs/users/cheat_sheet/)

## `C++`

### Generate `compile_commands.json`

```bash
buck2 targets //path/to/rule:target#compilation-database --show-output
```
Example output:
```
File changed: root//compile_commands.json
Build ID: 212db4b0-f1e0-40bf-916d-d7a95bc5f6df
Jobs completed: 4. Time elapsed: 0.0s.
root//path/to/rule:target[compilation-database] buck-out/v2/gen/root/904931f735703749/__1__/compilation-database/compile_commands.json
```

Note that only the last line is sent to stdout. To copy this file to the current directory:

```
buck2 targets //path/to/rule:target#compilation-database --show-output | cut -d " " -f 2 | xargs -I {} cp {} .
```

### Rules

The most common rules are:

* [cxx binary](https://buck2.build/docs/prelude/globals/#cxx_binary)
* [cxx genrule](https://buck2.build/docs/prelude/globals/#cxx_genrule)
* [cxx library](https://buck2.build/docs/prelude/globals/#cxx_library)
* [cxx test](https://buck2.build/docs/prelude/globals/#cxx_test)

## Rust

### Reindeer

Generate build files based on `Cargo.toml` files

[repo](https://github.com/facebookincubator/reindeer/)

[docs](https://github.com/facebookincubator/reindeer/blob/main/docs/MANUAL.md)

### Steve Klabnik's Blog

In May 2023 Steve put together a series of blog posts on working with `rust` / `reindeer` / `buck2` that were very good:

* [Using buck to build Rust projects](https://steveklabnik.com/writing/using-buck-to-build-rust-projects)
* [Using Crates.io with Buck](https://steveklabnik.com/writing/using-cratesio-with-buck)
* [Updating Buck ](https://steveklabnik.com/writing/updating-buck)
