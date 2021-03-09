# External Packages
By using [[Cargo]] and [[Use]] we can bring external packages into our projects.

Cargo.toml
```toml
[dependencies]
rand = "0.5.5"
```

```rust
use rand::Rng;

fn main() {
	let secret_number = rand::thread_rng().gen_range(1,101);
}
```

## `std`
Although `std` is an external package it doesn't need to be included in *Cargo.toml* since it's shipped with Rust. 

To import Hashmap:
```rust
use std::collections::HashMap;
```