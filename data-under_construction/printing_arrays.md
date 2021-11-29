
# Pringting Arrays in Rust
Lets look at the simple task of printing an array to terminal:

```rust

  fn main(){

    let a: [i32; 5] = [1, 2, 3, 4, 5];
    println!("{}",a);

}//--main

```
We are getting an error about printing a.
```
i32; 5]
let a: [i32; 5] = [1, 2, 3, 4, 5];
`[i32; 5]` doesn't implement `std::fmt::Display`

`[i32; 5]` cannot be formatted with the default formatter

help: the trait `std::fmt::Display` is not implemented for `[i32; 5]`
```
Display is a trait. To be printed out by println macro, the object needs to implement this trait.
We can still print the array since println also use another trait for printing and that is "Debug" trait. To need to tell the println macro to use the Debug implementation and print the object. For this we just have to chage following:
```
    println!("{:?}",a);
```
