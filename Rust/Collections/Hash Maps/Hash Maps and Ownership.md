# Hash Maps and Ownership
For types with the [[Copy Trait]] like [[Integers]], the values are copied into a hash map. For [[Ownership|owned]] values like [[String]], the values will be moved and the hash maps will own the values.

```rust
use std::collections::HashMaps;

let field_name = String::from("Favorite color");
let field_value = String::from("Blue");

let mut map = HashMap::new();
map.insert(field_name, field_value);
// field_name and field_value are invalid at this point as they are moved.
```