# Return Values From Loops
one use of a loop is to retry an operation that might fail. You might need to return that value to the rest of the code. After a `break` you can return a value.
```rust
fn main() {
	let mut counter = 0;
	
	let result = loop {
		counter += 1;
		
		if counter == 10 {
			break counter * 20;
		}
	};
	
	println!("The result is {}", result);
}
```
will print a result of 20.