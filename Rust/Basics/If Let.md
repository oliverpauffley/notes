# If Let
Using `if let` is a less verbose way to handle a [[Match]] pattern where you only care about one value.
```rust
let some_u8_value = Some(0u8);
match some_u8_value {
	Some(3) => println!("three"),
	_ => (),
}
```
becomes
```rust
if let Some(3) = some_u8_value {
	println!("three");
}
```

You can also include an `else` 

```rust
let mut count = 0;
if let Coin::Quarter(state) = coin {
	println!("state quarter from {:?}!", state);
	
} else {
	count += 1;
}
```