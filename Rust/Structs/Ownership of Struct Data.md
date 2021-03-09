# Ownership of Struct Data
It is possible to use [[References]] in [[Structs]] rather than having a Struct take [[Ownership]]  of it's data. However it requires the use of [[Lifetimes]]. 

The following will **not** work as the lifetimes have not be set.

```rust
struct User {
	username: &str,
	email: &str,
}
```
