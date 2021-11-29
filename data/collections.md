# Collections
Collections unlike the built-in array and tuple types, the data these collections point to is stored on the heap, which means the amount of data does not need to be known at compile time and can grow or shrink as the program runs.
Strings are implemented as a collection of bytes, plus some methods to provide useful functionality when those bytes are interpreted as text.

### Appending to a String with push_str and push
```rust
 let mut s = String::from("foo");
    s.push_str("bar");
```
In the fol code if the push_str method took ownership of s2, we wouldn’t be able to print its value on the last line. However, this code works as we’d expect!
```rust
 let mut s1 = String::from("foo");
    let s2 = "bar";
    s1.push_str(s2);
    println!("s2 is {}", s2);
```    
The push method takes a single character as a parameter and adds it to the String.

### Concatenation with the + Operator or the format! Macro
```rust
fn main() {
    let s1 = String::from("Hello, ");
    let s2 = String::from("world!");
    let s3 = s1 + &s2; // note s1 has been moved here and can no longer be used
}
```
For more complicated string combining, we can use the format! macro:
```rust
fn main() {
    let s1 = String::from("tic");
    let s2 = String::from("tac");
    let s3 = String::from("toe");

    let s = format!("{}-{}-{}", s1, s2, s3);
}
```
This code also sets s to tic-tac-toe. The format! macro works in the same way as println!, but instead of printing the output to the screen, it returns a String with the contents. The version of the code using format! is much easier to read, and the code generated by the format! macro uses references so that this call doesn’t take ownership of any of its parameters.

### Indexing into Strings
In many other programming languages, accessing individual characters in a string by referencing them by index is a valid and common operation. However, if you try to access parts of a String using indexing syntax in Rust, you’ll get an error. Consider the invalid code in Listing 8-19.

This code does not compile!
```rust
    let s1 = String::from("hello");
    let h = s1[0];
```
> ** A String is a wrapper over a Vec<u8> **
*The u8 is for one byte of 8 bits a UTF-8 encoding can take from 1 to 4 bytes for a letter. Most freq used letters use less bytes and less freq letter take more bytes*