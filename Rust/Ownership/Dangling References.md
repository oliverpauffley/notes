# Dangling References
In languages with pointer's it's easy to create a *dangling pointer*, where the reference is a location where the memory might have already been de-allocated. Rust guarantees this won't happen by using [[Lifetimes]].

```rust
fn main() {
	let reference_to_nothing = dangle();
}

fn dangle() -> &String { // dangle returns a reference to a String

	let s = String::from("hello"); // s is a new String
	
	&s // we return a reference to s.
} // Here, s goes out of scope and is dropped!
```

The easy solution is to pass the [[Ownership]] out by returning the String directly

```rust
fn no_dangle() -> String {
	let s = String::from("hello");
	
	s
}
```
