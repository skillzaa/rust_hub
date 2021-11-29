# Slices
Another data type that does not have ownership is the slice. Slices let you reference a contiguous sequence of elements in a collection rather than the whole collection.
A string slice is a reference to part of a String, and it looks like this:
```rust
 let s = String::from("hello world");

    let hello = &s[0..5];
    let world = &s[6..11];
```
if your slice includes the last byte of the String, you can drop the trailing number. 
```rust
let slice = &s[3..];
```
You can also drop both values to take a slice of the entire string.
```rust
let slice = &s[..];
```
### String Literals Are Slices
The type of s here is &str: it’s a slice pointing to that specific point of the binary. This is also why string literals are immutable; &str is an immutable reference.

```rust
let s = "Hello, world!";
```
I think functions should take &str (string slices) as argument rather than String.

> A slice is a slice from a continuous sequence of memory. We can have slices of any vector or array. The &str type is just a slice of some string.

