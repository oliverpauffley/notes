# Updating a Hash Map
## Overwriting a Value
```rust
scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Blue"), 25);
```
## Only Inserting a Value If the Key Has No Value
```rust
use std::collections::HashMap;

let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10);

scores.entry(String::from("Yellow")).or_insert(50);	
scores.entry(String::from("Blue")).or_insert(50);	

print!("{:?}", scores);
```
Here "Blue" will remain as `10` since it already exists and is not overwritten.
The `entry` method returns an [[Enums|Enum]] `Entry` which represents a value which might or might not exist. The method `or_insert` returns the value or updates with the new value.
## Updating Based on the Old Value
To count how many times a word appears in a sentence:
```rust
use std::collections::HashMap;

let text = "hello world wonderful world";

let mut map = HashMap::new();

for word in text.split_whitespace() {
	let count = map.entry(word).or_insert(0); // mutable count references to the keys value.
	*count += 1;
}

println!("{:?}", map);
```