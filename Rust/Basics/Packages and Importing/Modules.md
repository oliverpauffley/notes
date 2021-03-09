# Modules
Define a module using the `mod` keyword.
```rust
mod front_of_house {
	mod hosting {
		fn add_to_waitlist() {}
		
		fnt seat_at_table() {}
	}
	
	mod serving {
		fn take_order() {}
		
		fn serve_order() {}
		
		fn take_payment() {}
	}
}
```
This creates the `front_of_house` module and then two internal modules as well. Modules can also contain [[Structs]], [[Enums]], [[Traits]] and [[Functions]].

## Module tree
```bash
crate
 └── front_of_house
     ├── hosting
     │   ├── add_to_waitlist
     │   └── seat_at_table
     └── serving
         ├── take_order
         ├── serve_order
         └── take_payment
```

[[Module Path]]