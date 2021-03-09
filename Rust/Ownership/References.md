# References 
To use a variable without passing [[Ownership]] use a reference
```rust
fn main() {
	let s1 = String::from("hello");
	
	let len = calculate_length(&s1);
	
	println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize { // s is a reference to a String
	s.len()
} // here s goes out of scope but it does not have ownership of what s refers to, nothing happens.
```

by passing in `&s1` with give the function a reference rather than the variable to avoid passing ownership. The opposite of references are [[Dereferences]]

We call having references as function parameters **borrowing**. As in real life, if a person owns something, you can borrow it from them. When you're done you have to give it back. If you try and change something that has been borrowed you will get an error!

This **doesn't work**
```rust
fn main () {
	let s = String::from("hello");
	
	change(&s);
}

fn change(some_string: &String) {
	some_string.push_str(", world");
}
```
as we are trying to change a borrowed value.

## Mutable References
To allow references to be changed when borrowed you have to use `mut`

```rust
fn main () {
	let mut s = String::from("hello");
	
	change(&mut s);
}

fn change(some_string: &mut String) {
	some_string.push_str(", world");
}
```
first we have to make `s` a `mut` then use `&mut` for a mutable reference.

### Restriction
You can only have one mutable reference to a piece of data. This means that rust can check for data races at compile time.A

## [[Dangling References]]