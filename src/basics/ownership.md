# Ownership

### Ownership Rules
1. Each value in Rust has a variable that’s called its owner.
2. There can only be one owner at a time.
3. When the owner goes out of scope, the value will be dropped.
---

We can consider **String** as a vector of chars. A String is always placed on *heap* that is why it can grow and shrink.
The ownership model is not much visible on variables placed on stack(mostly primtives) since it is inexpensive to copy them.

**String Literals** ie *&str* is not mutable. It is written in the code so can not be changed, however you can make copies of it and then change those.
To convert string from string literal
```rust
let s = String::from("hello");
or
let t = "hello".to_string();
```
Here we have declared a string literal, also known as a string slice.

String literals have a static lifetime, which means the string hello_world is guaranteed to be valid for the duration of the entire program. We can explicitly specify hello_world’s lifetime as well:
```rust
let hello_world: &'static str = "Hello, world!";
```
> How Rust creates a deep clone of a data structure ?

### The Copy trait
If a type implements the Copy trait, an older variable is still usable after assignment.

Rust won’t let us annotate a type with the Copy trait if the type, or any of its parts, has implemented the Drop trait. 

If the type needs something special to happen when the value goes out of scope and we add the Copy annotation to that type, we’ll get a compile-time error.

So what types implement the Copy trait? 

You can check the documentation for the given type to be sure, but as a general rule, any group of simple scalar values can implement Copy, and nothing that requires allocation or is some form of resource can implement Copy. Here are some of the types that implement Copy:

- All the integer types, such as u32.
- The Boolean type, bool, with values true and false.
- All the floating point types, such as f64.
- The character type, char.
- Tuples, if they only contain types that also implement Copy. 

For example, (i32, i32) implements Copy, but (i32, String) does not.

The semantics for passing a value to a function are similar to those for assigning a value to a variable. Passing a variable to a function will move or copy, just as assignment does.

Returning values can also transfer ownership.

>The ownership of a variable follows the same pattern every time: assigning a value to another variable moves it. When a variable that includes data on the heap goes out of scope, the value will be cleaned up by drop unless the data has been moved to be owned by another variable.

It’s possible to return multiple values from a function using a tuple.

The &s1 syntax lets us create a reference that refers to the value of s1 but does not own it. Because it does not own it, the value it points to will not be dropped when the reference stops being used.

We can have a mutable reference borrow.But mutable references have one big restriction: you can have only one mutable reference to a particular piece of data at a time. 

```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```
If the reference is not mutable we can have as many copies as we want.

### Dangling References
Following code creats a dangling pointer
```rust
fn main() {
    let reference_to_nothing = dangle();
}

fn dangle() -> &String {
    let s = String::from("hello");

    &s
}
```
Here is the correct code (Other than the main fn other smaller fn should return ownership)

```rust
fn no_dangle() -> String {
    let s = String::from("hello");

    s
}
```
### The Rules of References

- At any given time, you can have either one mutable reference or any number of immutable references.
- References must always be valid.