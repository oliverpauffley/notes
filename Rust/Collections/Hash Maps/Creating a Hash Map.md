# Creating a Hash Map

```rust
use std::collections::HashMap;

let mut scores = Hashmap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"),50);
```
> Note that all keys must be the same type and all values must be the same type.

## Using `collect`
By using the collect method you can iterate over vectors of tuples to fill a hash map.

```rust
use std::collections::HashMap;

let teams = vec![String::from("Blue"), String::from("Yellow")];

let initial_scores = vec![10, 50];

let mut scores: HashMap<_, _> = 
	teams.into_iter().zip(initial_scores.into_iter()).collect();
```