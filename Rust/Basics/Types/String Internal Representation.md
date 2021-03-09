## String internal Representation
A `String` is a wrapper over a [[Vec]] where the text is [[UTF-8]] encoded.
	
```rust
let hello = String::from("Hola");
```
In this case the `len` will be 4, which means that the vector storing the string is 4 [[Bytes]] long. Each letter takes 1 byte.

```rust
let hello = String::from("Здравствуйте");
```

In this case you might thing the length is 12. However, this string actually takes 24 bytes to encode. This is because each character takes 2 bytes of storage. This is the reason [[String#Why Indexing Doesn't Work]].