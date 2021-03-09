# Traits as Parameters
in [[Implementing a Trait on a Type]] we created the `Summary` trait. We can define a `notify` function that calls the summarize method on its `item` parameter using the `impl Trait` syntax.
```rust
pub fn notify(item: &impl Summary) {
	println!("Breaking news! {}", item.summarize());
}
```
This means we can pass in any type that implements the `Summary` trait.

## Trait Bound Syntax
The `impl Trait` syntax is shorthand for the following `trait bound` syntax

```rust
pub fn notify<T: Summary>(item: &T) {
	println!("Breaking news! {}", item.summarize());
}
```

the longer form is useful in complex cases, for example where we want to use the same type twice
```rust
pub fn notify<T: Summary>(item1: &T, item2: &T){
```

## Specifying Multiple Trait Bounds with the + Syntax
We can specify more than one trait bound. If we wanted our parameter so have the `Summary` and `Display` trait.
```rust
pub fn notify(item: &(impl Summary + Display)) {
```

## `where` Clauses
Using too many trait bounds can be hard to read. So instead using the `where` syntax can help.
```rust
fn some_function<T, U>(t: &T, u: &U) -> i32 
	where T: Display + Clone,
			   U: Clone + Debug
{
```