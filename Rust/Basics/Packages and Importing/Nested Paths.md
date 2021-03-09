# Nested Paths
When importing with [[Use]] you can use nested paths to avoid repetition
```rust
use std::cmp::Ordering;
use std::io;
```
becomes
```rust
use std::{cmp::Ordering, io};
```