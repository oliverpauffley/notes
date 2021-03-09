# Structs

```rust
struct User {
	username: String,
	email: String,
	sign_in_count: u64,
	active: bool,
}
```
> Note that the struct has [[Ownership]] over all of the [[String]] types.

We can then use this struct with concrete values

```rust
let user1 = User {
	email: String::from("someone@example.com"),
	username: String::from("someone"),
	active: true,
	sign_in_count: 1,
}
```
We can then access elements of the struct using `.` notation.
```rust
user1.email
```

When building a new instance, if the parameter names match you can omit them.

```rust
fn build_user(email: String, username: String) -> User {
	User {
		email,
		username,
		active: true,
		sign_in_count: 1,
	}
}
```

## Creating instances from other instances with update syntax
Rather than having to update all of the fields explicitly, we can use the `..` syntax to only update the fields we care about.
```rust
let user2 = User {
	email: String::from("anotheremail@example.com"),
	username: String::from("anotherusername"),
	..user1 // use the rest of user1 to create user2
}
```

## Tuple Structs
```rust
struct Color(i32, i32, i32);
struct Coordinate(i32, i32);

let black = Color(0,0,0);
let origin = Coordinate(0,0);
```
**Tuple Structs** let us create a tuple like struct that has unnamed fields but are their own type.

## [[Ownership of Struct Data]]
