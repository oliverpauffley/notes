# Use
The `use` keyword is a way of bringing function and modules into scope in a similar way to [[Module Path]]

```rust
mod front_of_house {
	pub mod hosting {
		pub fn add_to_waitlist() {}
	}
}

use crate::front_of_house::hosting;

pub fn eat_at_restaurant() {
	hosting::add_to_waitlist();
	hosting::add_to_waitlist();
	hosting::add_to_waitlist();
}
```

By using `use` we don't have to specify the full path every time we call the function.

> Note that you don't want to do the above with `use crate::front_of_house::hosting::add_to_waitlist;`. Since , although it would work we wouldn't have to add `hosting::` to call the function and it would become unclear where the function was defined.

## Renaming with use

we can rename as we import with use as follows

```rust
use std::fmt::Result;
use std::io::Result as IoResult;
```
which allows for importing something with the same name.