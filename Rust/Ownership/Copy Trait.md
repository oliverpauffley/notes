# Copy Trait
Rust has a special annotation called the `Copy` trait that we can place on types like integers that are stored on the stack. 

If a variable has the `Copy` trait:
- An older variable can still be usable after assignment.
- You cannot annotate will `Copy` if we already have defined a [[Drop Trait]].

## Copy Types
In general any group of similar scalar values can be `Copy` or something that doesn't required allocated memory.
- [[Integers]].
- Bools.
- [[Floats]].
- [[Char]].
- [[Tuple]]s if they only contain values that are also `Copy`. ie `(i32, i32)` is `Copy` but `(bool, String)` is not. 