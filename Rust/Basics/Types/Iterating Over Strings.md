# Iterating Over Strings
There are a number of ways to iterate over strings in rust

## `chars()` - returns each [[Unicode]] scalar
```rust
fn main() {
	for c in "नमस्ते".chars() {
    	println!("{}", c);
	}
}
```
will print:
```bash
न
म
स
्
त
े
```
## `bytes()` - returns the byte representation
```rust
fn main() {
	for b in "नमस्ते".bytes() {
	    println!("{}", b);
	}
}
```
will print:
```bash
224
164
// --snip--
165
135
```