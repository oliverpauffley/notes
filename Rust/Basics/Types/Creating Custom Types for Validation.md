# Creating Custom Types for Validation
We could create our own types the have built in validations when a new instance is created.
```rust
pub struct Guess {
	value: i32,
}

impl Guess {
	pub fn new(value: i32) -> Guess {
		if value < 1 || value > 100 {
			panic!("Guess value must be between 1 and 100, got {}.", value);
		}
	Guess {value}
	}
	
	pub fn value(&self) -> i32 {
		self.value
	}
}
```

> The function `value` is often called a *getter* as it allows you to access the private value within a guess. This is important so that you cannot set the value without using the `new` function.