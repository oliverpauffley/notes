# Packages and Crates
>A `crate` is a binary or library.
>The `crate root` is a source file that the compiler starts from and makes up the root module.

>a `package` is one or more crates that provide a set of functionality. It contains a cargo.toml file that describes how to build those crates.

## Rules
- A package must contain zero or one library crate.
- it can contain as many binary crates as you need, but must contain at least one.
- *src/main.rs* is the crate root of a binary crate with the same name as the package.
- similarly with *src/libs.rs* for library packages.

[[Modules]] allow you to create library crates.