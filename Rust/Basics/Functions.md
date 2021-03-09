# Functions
functions in rust are `snake_case`

```rust
fn a_function() {
}
```

## Return Values
You can return values from functions with a `->` like so
```rust
fn add(x: i32, y: i32) -> i32 {
	x + y
}
```
note that you can use the keyword `return` but it is not necessary. Note that the function is an [[Expressions]].