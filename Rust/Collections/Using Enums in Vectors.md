# Using [[Enums]] in [[Vector]]s
By using an enum you can store values in a vector that are of different underlying types.

```rust
enum SpreadsheetCell {
	Int(i32),
	Float(f64),
	Text(String),
}

let row = vec![
	SpreadsheetCell::Int(3),
	SpreadsheetCell::Text(String::From("blue")),
	SpreadsheetCell::Float(10.12),
];
```