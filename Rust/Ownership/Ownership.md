# Ownership
## Rules
- Each value in Rust has a variable that's called its *owner*.
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped.

## Variable Scope
scope works like other programming languages.
```rust
{ // s is not valid here
	let s = "hello"; // s is now valid.
} // the scope for s is now over so s is invalid.
```
## [[String]] Type
The [[String]] type is a good example to see the concept of ownership in action in rust

## With Functions
```rust
fn main() {
	let s = String::from("hello"); // s comes into scope
	
	takes_ownership(s);  // s's value moves into the function ...
						 // ... and is no longer valid here
						 
	let x = 5;           // x comes into scope
	
	makes_copy(x);       // x would be moved into the function,
	                     // but i32 is Copy so is still ok to use.
						 
} // Here, x goes out of scope but s has already been moved and invalidated 

fn takes_ownership(some_string: String) { // some_string comes into scope
	println!("{}", some_string);
} // Here, some_string goes out of scope and 'drop' is called. The backing 
  // memory is freed.
  
fn makes_copy(some_integer: i32) { // some_integer comes into scope
	println!("{}", some_integer);
} // Here, some_integer goes out of scope but has no 'drop' method.
```
if we tried to use `s` after the `takes_ownership` is called we would get a compile error. However, `x` is safe to use after the `makes_copy` call.

## Return Values and Scope
```rust
fn main() {
	let s1 = gives_ownership(); 	// gives ownership by returning s1
	
	let s2 = String::from("hello"); // s2 comes into scope
	
	let s3 = takes_and_gives_back(s2); // s2 is moved into 
									   // function, which then moves 
									   // it's return value into s3
									   
} // Here, s3 goes out of scope and is dropped. s2 goes out of scope but was already moved. s1 goes out of scope and is dropped.

fn gives_ownership() -> String { // will move its return value into
								 // the function that calls it
	let some_string = String::from("hello");
	
	some_string				// return and moves into calling func
}

fn takes_and_gives_back(a_string: String) -> String { // a_string comes into scope
	a_string 										  // a_string is moved
}