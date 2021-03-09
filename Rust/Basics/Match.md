# Match
The match statement is like a [[Switch]] in go. 

```rust
match guess.cmp(&value) {
	Ordering:Less...,
	Ordering::Greater...,
	Ordering::Equal...,
}
```
a value can be compared to a series of patterns or [[Enums]].

```rust
enum Coin {
	Penny,
	Nickel,
	Dime,
	Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
	match coin {
		Coin::Penny => 1,
		Coin::Nickel => 5,
		Coin::Dime => 10,
		Coin::Quarter => 25,
	}
}
```

## Binding to values
```rust
#[derive(Debug)]
enum UsState {
	Alabama,
	Alaska,
	...
}

enum Coin {
	Penny,
	Nickel,
	Dime,
	Quarter(UsState),
}
```
Which can then be bound from the match statement:
```rust
fn value_in_cents(coin: Coin) -> u8 {
	match coin {
		Coin::Penny => 1,
		Coin::Nickel => 5,
		Coin::Dime => 10,
		Coin::Quarter(state) => {
			println!("State quarter from {:?}!", state);
			25
		}
	}
}
```

## Matching with [[Option]]
If we want to deal with the `Option` enum where a value can be something or nothing the we need to use `match`.

```rust
fn plus_one(x: Option<i32) -> Option<i32> {
	match x {
		None => None,
		Some(i) => Some(i + 1),
	}
}

let five = Some(5);
let six = plus_one(five);
let none = plus_one(None);
```

## Matches are Exhaustive
When using a match it **must** cover all cases. The following will not compile.
```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
	match x {
		Some(i) => Some(i + 1)
	}
}
```
## _ Placeholder
use `_` when you want a wildcard match that matches anything that hasn't been defined.

```rust
let some_u8_value = 0u8;
match some_u8_value {
	1 => println!("one");
	3 => println!("three");
	5 => println!("five");
	_ => (),
}
```