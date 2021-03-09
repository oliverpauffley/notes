# Strings (Memory)
```rust
let s1 = String::from("hello");
let s2 = s1;
```
You might assume that the value 'hello' is just copied between the two variables `s1` and `s2` but since [[String]]s are stored on the heap the behavior is different. A [[String]] is actually made up of three parts; a pointer to the memory that holds the contents of the string; a length; and a capacity. This information is stored on the stack. 
![[string_ptr_1.svg]]

- length is the memory in bytes currently being used.
- capacity is the total amount of memory in bytes that has been allocated.

When we assign `s2 = s1` the `String` data is copied, meaning the pointer, length and capacity that are on the stack. We do not copy the heap data. 
![[string_ptr_2.svg]]

However rust goes further by also deleting the old `s1` variable to avoid having two variables pointing to the same heap memory. So really the `s2 = s1` actually *moves* the data like so:
![[string_ptr_3.svg]]

This means that data is not copied and we are safe to only use the valid `s2` variable and will get an error if we try to use `s1` after the move.

This behavior can be avoided with [[Clone]]