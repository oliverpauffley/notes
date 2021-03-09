# Generics and [[Enums]]
The `Option<T>` is an example of a generic enum.
```rust
enum Option<T> {
	Some(T),
	None,
}
```

We can also have enums over multiple generic types

```rust
enum Result<T, E> {
	Ok(T),
	Err(E),
}
```