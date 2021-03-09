# Accessing Values in a Hash Map
```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

let team_name = String::From("Blue");
let score = scores.get(&team_name);
```

The returned value is wrapped as a [[Option]]. Since if you `get` for a value with no key it will return `None`.

# Iterating Over a Map
```rust
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

for (key, value) in &scores {
	println!("{}: {}", key, value);
}
```