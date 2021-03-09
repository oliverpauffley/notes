# Unrecoverable Errors
When the `panic!` macro executes, the program will print a message, unwind and clean up the stack before quitting. 

> This unwinding adds to the binary size. by including
> ```toml
> [profile.release]
> panic =abort
> ```
> you can skip the unwinding step.

```rust
fn main() {
	panic!("crash and burn")
}
```