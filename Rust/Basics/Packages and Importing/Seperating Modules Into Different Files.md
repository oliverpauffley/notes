# Separating Modules into Different Files

Rust can keep functions in different files.  Uses the same syntax as [[Module Path]] and [[Modules]].

src/lib.rs:
```main
mod front_of_house;

pub use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
	hosting::add_to_waitlist();
}
```

src/front_of_house.rs:
```rust
pub mod hosting;
```

src/front_of_house/hosting.rs:
```rust
pub fn add_to_waitlist() {}
```

tree:
```
src
├── front_of_house
│   └── hosting.rs
├── front_of_house.rs
└── main.rs
```
