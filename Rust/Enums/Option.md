# Option Enum
The Option [[Enums]] is defined in the [[Rust]] standard library. `option` captures the idea of a value that could be something or could be nothing. This enforces the compiler to check you have dealt with all cases. This replaces the idea of [[Null]] in other languages.

```rust
enum Option<T> {
	Some(T),
	None,
}
```
the `<T>` syntax represent a the [[Generics]] type syntax. This means that the `Some(T)` can hold a parameter of any type. 

```rust
let some_number = Some(5);
let some_string = Some("a string");

let absent_number: Option<i32> = None;
```

Note that something like the following **doesn't** work

```rust
let x: i8 - 5;
let y: Option<i8> = Some(5);

let sum = x + y;
```
since even though we have set the value of `y` to be something we haven't checked that y is not `None`. Instead we need to use [[Match]] decide what to do if y is `None`.