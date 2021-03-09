# Expressions
expressions in rust return a value.
```rust
let x = {
	let y = 3;
	y + 1
}
```
it looks like this is missing a semi-colon in the line `y + 1` but this is important as it allows a value to be returned. If you add a semi-colon you would turn the expression into a [[Statements]].