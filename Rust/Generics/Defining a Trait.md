# Defining a Trait
A type's behavior consists of the methods we can call on that type. Different types share the same behavior if we can call the same methods on all of the types. Trait definitions are a way to group method signatures together to define a set of behaviors necessary to accomplish some purpose.

## Example
We might have multiple structs that hold various kinds and amounts of text: A `NewsArticle` or a `Tweet`. We want to make a media aggregator library that can display summaries of data that might be stored in a `NewsArticle` or `Tweet` instance. To do this, we need a summary from each type, and we need to request that summary by calling a `summarize` method on an instance.

```rust
pub trait Summary {
	fn summarize(&self) -> String;
}
```
> continued in [[Implementing a Trait on a Type]]

## Default implementations
Sometimes it's useful to have a default behavior for all or some of the methods. These can then be overwritten as needed.

```rust
pub trait Summary {
	fn summarize(&self) -> String {
		String::from("(Read more...)") // by defining a method here we create a default.
	}
}
```
Then to use the default implementation
```rust
impl Summary for NewsArticle {}
```
