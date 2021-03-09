# Returning Types that Implement Traits

We can also use the `impl Trait` syntax in the return position.
```rust
fn retruns_summarizable() -> impl Summary {
	Tweet {
		username: String::from("horse_ebooks"),
		content: String::from(
			"some content"
		),
		reply: false,
		retweet: false,
	}
}
```

This is especially useful for [[Closures]] and [[Iterators]]

> Note that this only works if the function can only return one type.