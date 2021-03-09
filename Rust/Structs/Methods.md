# Methods

To define a method create and [[Implementation Block]] with `impl` and then define functions within the block.

```rust
struct Rectangle {
	width: u32,
	height: u32,
}

impl Rectangle {
	fn area(&self) -> u32 {
		self.width * self.height
	}
	
	fn can_hold(&self, other: &Rectangle) -> bool {
		self.with > other.width && self.height > other.height
	}
}

rect1 = Rectangle {
	width: 30,
	height: 50,
}

rect1.area()
```

## Associated Functions
Another useful feature is creating methods in [[Implementation Block]]s that **don't** take self as a parameter.  They are often used as constructors to return a new instance of a struct.

```rust
impl Rectangle {
	fn square(size: u32) -> Rectangle {
		Rectangle {
			width: size,
			height: size,
		}
	}
}
```
Which is then called like
```rust
let sq = Rectangle::square(3)
```
