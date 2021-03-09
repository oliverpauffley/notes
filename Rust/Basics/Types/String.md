# String

The type `String` is stored on heap so is able to store an amount of text that is unknown at compile time. You can create a `String` from a string literal like so.
```rust
let s = String::from("hello");
```
> `String::` means that the `from` function is from the `String` type. 

This kind of string can be mutated.
```rust
let mut s = String::from("hello");

s.push_str(", world!"); // push_str() appends a literal to a string.

println!("{}", s); // will print 'hello, world!'.
```
This is important as `Strings` can be changed but string literals [[Slice]] cannot.

## [[Creating a New String]]

## [[Updating a String]]

## Memory and allocation

With a string literal the text is hard-coded into the final executable as it's immutable. But if you want this to be flexible at compile time this wont work. This means that we need to allocate some memory on the heap (unknown size).
- The memory must be requested form the memory allocator.
- We need a way of returning this memory to the allocator once we are done.

In go this handled using the [[Garbage Collector]] and in C this is done with `malloc` and `free`. Both have issues but C is tricky with where you place your free's and malloc. 

Instead in Rust the memory is automatically returned once the variable that owns it goes out of [[Ownership#Variable Scope]]. Rust automatically calls a special function called [[Drop]] that returns the memory. Rust calls `drop` automatically at the end of the closing curly brackets.

[[Strings (Memory)]]

## Why Indexing Doesn't Work
If you try:
```rust
let s1 =  String::from("hello");
let h = s1[0];
```
The rust compiler will error that you cannot index strings. This is because of the underlying way that strings are [[String Internal Representation|represented]].

## Slicing Strings
You can slice a string using the `[]` syntax but be aware that this can cause runtime panics.

```rust
fn main() {
let hello = "Здравствуйте";
let s = &hello[0..4];
}
```
The above is valid since `0..4` returns a valid character but if you tried to use `0..1` the code would panic.

## [[Iterating Over Strings]]