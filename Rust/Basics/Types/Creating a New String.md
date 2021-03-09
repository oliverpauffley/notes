# Creating a New String
```rust
let mut s = String::new();
```
## Creating from Initial Data
```rust

let data = "initial contents";

let s = data.to_string(); 

// or directly
let s = "initial contents".to_string();
```
This works on any type that has the `Display` [[Traits]].
or using `String::from`
```rust
let s = String::from("initial contents")
```

Both work the same so it's a matter of style.



