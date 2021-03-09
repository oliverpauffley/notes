# Debug Printing
Trying to print a struct as follows will fail.

```rust
struct Rectangle {
	width: u32,
	height: u32,
}

let rect1 = Rectangle {
	width: 30,
	height: 50,	
};

println!("rect1 is {}", rect1);
```
The compiler will complain that `the trait 'std::fmt::Display' is not implemented by Rectangle`. Since this [[Traits]] is not implemented we can't print with `println!`. However if we use `println!("rect1 is {:?}",rect1)` and [[derive]] the Debug [[Traits]] we can then print a debug output.

```rust
#[derive(Debug)]
struct Rectangle {
	width: u32,
	height: u32,
}
```