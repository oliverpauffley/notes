# Making Structs and Enums Public
We can use the `pub` keyword to set [[Enums]] and [[Structs]] as public. 

## Struct

If we use `pub` before a struct definition, we make the struct public, but the struct's fields will still be private. Each field is handled on a case-by-case basis.

```rust
mod back_of_house {
	pub struct Breakfast {
		pub toast: String, // public field
		seasonal_fruit: String, // private
	}
	
	impl Breakfast {
		pub fn summer(toast: &str) -> Breakfast {
			Breakfast {
				toast: String::from(toast),
				seasonal_fruit: String::from("peaches"),
			}
		}
	}
}

pub fn eat_at_restaurant() {
	// Order a breakfast in the summer with Rye toast
	let mut meal = back_of_house::Breakfast::summer("Rye");
	// Change our mind about which bread.
	meal.toast = String::from("Wheat");
	println!("I'd like {} toast please", meal.toast);
	
	// This won't work as the fruit is private.
	// meal.seasonal_fruit =  String::from("blueberries");
}
```

Also note that we have to provide a function to set the fruit as it's private.

## Enum

```rust
mod back_of_house {
	pub enum Appetizer {
		Soup,
		Salad,
	}
}

pub fn eat_at_restaurant() {
	let order1 = back_of_house::Appetizer::Soup;
}
```
However the default for enums is to be public.