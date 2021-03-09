# Conditionally Implement Methods
By using a trait bound with an `impl` block that uses generic type parameters, we can implement methods conditionally for types that implement the specified traits.

In the following example, the type `Pair<T>` always implements the new function. But `Pair<T>` only implements the `cmp_display` method if its inner type `T` implements the `PartialOrd` Trait and the `Display` trait.

```rust

use std::fmt::Display; 

struct Pair<T> {
	x: T,
	y: T,
}

impl <T> Pair<T> {
	fn new(x: T, y: T) -> Self {
		Self { x, y }
	}
}

impl<T: Display + PartialOrd> Pair<T> {
	fn cmp_display(&self) {
		if self.x >= self.y {
			println!("The largest member is x = {}", self.x)
		} else {
			println!("The largest member is y = {}", self.y)
		}
	}
}
```

## Blanket Implementations
It is also possible to conditionally [[Implementing a Trait on a Type| implement a trait]] for any type that implements another trait. An example of the this is the `ToString` trait in the standard library that is implemented on any type that implements the `Display` trait.

```rust
impl<T: Display> ToString for T {
	// some code
}
```