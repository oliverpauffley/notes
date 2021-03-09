# Array
Arrays are a **fixed** length list of values of all the same type. 

```rust
let a = [1,2,3,4,5];
```

[[Vector]]s are similar types but **are** allowed to change length.

## With type
```rust
let a: [i32; 5] = [1,2,3,4,5];
```
## Accessing Array Elements
```rust
let a = [1,2,3,4,5];

let first = a[0];

let last = a[4];
```