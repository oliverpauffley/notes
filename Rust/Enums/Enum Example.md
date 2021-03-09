# Enum Example
An example of an enum that uses multiple types is as follows:

```rust
enum Message {
	Quit, // no data
	Move { x: i32, y: i32 }, // an anonymous struct
	Write(string), // a single value
	ChangeColor( i32, i32, i32), // multiple values
}
```
We can also implement [[Methods]] on enums

```rust

impl Message {
	fn call(&self) {
		// define method here
	}
}

let m = Message::Write(String::from("hello"));

m.call();
```