# Updating a String
### Appending a string slice
Just like [[Vector]]s and other [[Common Collections]] strings can grow in size.
```rust
let mut s = String::from("foo");
s.push_str("bar");
```
note that `push_str` takes a string [[Slice]] since we don't want to take ownership of the of parameter.
```rust
let mut s1 = String::from("foo");
let s2 = "bar";
s1.push_str(s2); // s2 is still in scope.
println!("s2 is {}", s2);
```
### Appending a character
```rust
let mut s = String::from("lol");
s.push('l');
```
### Concatenation
```rust 
let s1 = String::from("Hello, ");
let s2 = String::from("world!");
let s3 = s1 + &s2; // note that s1 has been moved here so it is out of scope.
```
> Note that under the hood the `+` operator uses the the `add` method `fn add(self, s: &str) -> String`. This means that the string we pass in is changed to a `&str` using [[Coercion]], specifically [[Deref Coercion]].

>Also note that this is an efficient operation since `let s3 = s1 + &s2;` takes ownership of `s1`, appends a copy of the contents of `s2` and returns [[Ownership]] of the result.

#### Using `format!`
It would be unwieldy to use `+` for multiple strings so instead we use the `format!` [[Macros]].
```rust
let s1 = String::from("tic");
let s2 = String::from("tac");
let s3 = String::from("toe");

let s = format!("{}-{}-{}", s1, s2, s3);
```