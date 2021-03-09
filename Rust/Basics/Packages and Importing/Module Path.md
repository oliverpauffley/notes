# Module Path
A path can take two forms:
- An *absolute path* starts from a crate root by using a crate name or a literal `crate`.
- A *relative path* starts from the current module and uses `self`, `super`, or an identifier in the current module.
Both absolute and relative paths are followed by one or more identifiers separated by double colons (::).

by using the [[pub]] key word to expose the function in the public api. 

```rust
mod front_of_house {
	mod hosting {
		fn add_to_waitlist() {}
	}
}

pub fn eat_at_restaurant() {
	// Absoulute path
	crate::front_of_house::hosting::add_to_waitlist();
	
	// Relative path
	front_of_house::hosting::add_to_waitlist();
}
```
Absolute path is preferred since you are more likely to move code definitions and item calls independently of each other.

## Super
You can also construct relative paths that begin in the parent module using `super`. It's like starting a file system path with `..`.

```rust
fn serve_order() {}

mod back_of_house {
	fn fix_incorrect_order() {
		cook_order();
		super::serve_order();
	}
	
	fn cook_order() {}
}
```

