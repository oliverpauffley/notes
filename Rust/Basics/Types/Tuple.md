# Tuple
a tuple is a general way of grouping a number of values together. They have a fixed length that cannot change. The values don't have to all have the same type.

```rust
let tup: (i32, f64, bool) = (500, 6.4, false);
```

values can be **de-structured** from a tuple like so

```rust
let tup = (500, 6.4, 1);

let (x, y, z) = tup;

println!("The value of y is: {}", y) // 6.4
```

or values can be grabbed through their index:
```rust
let x = (500, 6.4, 1);

let five_hundred = x.0;

let one = x.2;
```