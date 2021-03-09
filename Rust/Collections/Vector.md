# Vector
Note that vectors can only store values of the same type.
## Creating a New Vector
```rust
let v: Vec<i32> = Vec::new();
```
Or more typically the type is inferred.
```rust
let v = vec![1,2,3];
```
## Updating A Vector
```rust
let mut v = Vec::new();
v.push(5);
v.push(6);
```
Note that the variable must be mutable.
## Dropping a vector drops its elements
A vector is freed when it does out of scope.
```rust
{
	let v = vec![1,2,3,4];
	
}// <- v goes out of scope and is freed as well as
// the elements in v.
```
## Reading Elements of Vectors
```rust
let v = vec![1,2,3,4,5];

let third = &v[2];

// or

match v.get(2) {
	Some(third) => println!("The third element is {}", third),
	None => println!("There is no third element."),
}
```
## Iterating over the Values in a Vector
```rust
let v = vec![100, 32, 57];
for i in &v {
	println!("{}", i);
}
```
If you need to mutate each element.
```rust
let mut v = vec![100, 32, 57];
for i in &mut v {
	*i += 50;
}
```

