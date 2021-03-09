# Enums

Enums are used to *enumerate* all the different possible options for a variable. 

## Defining
```rust
enum IpAddrKind {
	V4,
	V5,
}
```
## Using
```rust
let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
```
## Associated Values
You can associate values to an enum and even associate different types to different enum values

```rust
enum IpAddr {
	V4(String)
	V6(String)
}
```
since V4 ip addresses always have four numeric parts
```rust
enum IpAddr {
	V4(u8, u8, u8, u8)
	V6(String)
}
```

You can even assign [[Structs]] as associated values to enums.

[[Enum Example]]