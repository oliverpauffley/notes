# Clone
Rather than moving like in [[Strings (Memory)]] we can clone data using the common method called `clone`. 
```rust
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {}, s2 = {}", s1, s2);
```
> This might be expensive as the data **is copied**.

## Cloning stack data
```rust
let x = 5;
let y = x;

println!("x = {}, y = {}", x, y);
```
This looks like it shouldn't work as x will be invalidated by setting `y = x`. However since integers are always stored on the stack there is no point in doing this. Instead stack data is always cloned. This is because Integers have the [[Copy Trait]]. 