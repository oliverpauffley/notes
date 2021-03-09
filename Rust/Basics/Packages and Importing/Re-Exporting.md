# Re-exporting
By combining [[Use]] and [[Public]] we can allow something to call something within our code that has been defined in another scope.

```rust
mod front_of_house {
	pub mod hosting {
		pub fn add_to_waitlist() {}
	}
}

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
	hosting::add_to_waitlist();
}
```

This means that you can organize code internally in way that makes sense whilst still being able to present a nice interface for code that imports this module.