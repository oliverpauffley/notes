# Slice
a slice is another data type that does not have ownership. Slices let you reference a contiguous sequence of elements in a collection rather than the whole collection.

## String Slice
a  *string slice* is a reference to part of a [[String]]
```rust
let s = String::from("hello world");

let hello = &s[0..5];
let world = &s[6..11];
```
The `[0..5]` bit means we reference a slice of the whole `String`.

![[Rust/Basics/Types/string_slice.svg]]

you can also drop the `0`. `[0..5] = [..5]` or similar for the last character `[3..len] = [3..]`.

so to return the first word from a string you could:
```rust
fn first_word(s: &String) -> &str { // str is a string slice
	let bytes = s.as_bytes();
	
	for (i, &item) in bytes.iter().enumerate() {
		if item == b' ' {
			return &s[0..i];
		}
	}
	
	&s[..]
}
```