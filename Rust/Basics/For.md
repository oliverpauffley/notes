# For
To loop over the elements in an array use a `for` loop.
```rust
fn main() {
	let a = [10, 20, 30, 40, 50];
	
	for element in a.iter() {
		println!("the value is: {}", element);
	}
}
```

you can also loop over an range (in this case in reverse order using a method).
```rust
fn main() {
	for number in (1..4).rev() {
		println!("{}!".number);
	}
	println!("LIFTOFF!!!");
}
```