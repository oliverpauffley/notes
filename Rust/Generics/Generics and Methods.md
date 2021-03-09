# Generics and Methods
```rust
struct Point<T> {
	x: T,
	y: T,
}

impl <T> Point<T> {
	fn x(&self) -> &T {
		&self.x
	}
}

fn main() {
	let p = Point { x: 5, y: 10};
	
	println!("p.x = {}", p.x());
}
```
Note that we have to include `impl<T>` to specify that we're implementing methods on the type `Point<T>`. 

We could implement methods only on `Point<f32>` like so
```rust
impl Point<f32> {
	fn distance_from_origin(&self) -> f32 {
		(self.x.powi(2) + self.y.powi(2)). sqrt()
	}
}
```

This means that the type `Point<f32>` will have a method named `distance_from_origin` and other instances of `Point<T>` will not have this method defined.

## With Mixed Types
We don't always have to have the same type as in the struct definition. This this example the method `mixup` acts on the `Point<T,U>` The method takes another `Point` which might have different types from the `self Point` were calling `mixup` on.
```rust
struct Point<T, U> {
	x: T,
	y: U,
}

impl <T, U> Point<T, U> {
	fn mixup <V, W>(self, other: Point<V, W>) -> Point<T,W> {
		Point {
			x: self.x,
			y: other.y,
		}
	}
}

fn main() {
	let p1 = Point { x: 5, y: 10.4};
	let p2 = Point { x: "Hello", y: 'c' };
	
	let p3 = p1.mixup(p2);
	
	println!("p3.x = {}, p3.y = {}", p3.x, p3.y);
}
```