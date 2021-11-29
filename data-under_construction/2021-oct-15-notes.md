# 2021-oct-15 Rought Notes
Cargo is Rust’s build system and package manager.

``` rust
$ cargo --version
```
### Creating a Project with Cargo
```rust
$ cargo new hello_cargo
$ cd hello_cargo
```
We set different flags in command line tools "software that we run from command line". There must be a place where these values are stored however once a command line tool is installed we set the flags from command line and do not directly access the storage place / file. These flags are internal to the tool. On the other hand there are some command line tools that need the presence of some file to read data from e.g web-pack , gulp etc.

### To run project 
```rust
$ cargo build // just build 
//or
$ cargo run // to build and run it
//or
$ cargo check // This command quickly checks your code to make sure it compiles but doesn’t produce an executable
//or
cargo build --release //  This command will create an executable in target/release instead of target/debug
``` 
Details about rust std library prelude @future. [https://doc.rust-lang.org/std/prelude/index.html](https://doc.rust-lang.org/std/prelude/index.html)
Some of std library features are implicitly available by a special std::prelude that is automatically used (along with a reference to the std crate) without declaration. The prelude contains functionality that virtually all code is likely to use and therefore Rust spares code from having to import it.

```rust
// You don't need these
extern crate std;
use std::prelude::*;
```
To use io lib you can
```rust
use std::io; //import the io lib
//or write directly
std::io::stdin;

```
Like variables, references are immutable by default
How to generate a random number
```rust
use std::io;
use rand::Rng;

fn main() {   
    let secret_number = rand::thread_rng().gen_range(1..101);
    println!("The secret number is! {}",secret_number);
}
```
- In the above code **rand** is crate,The **Rng trait** defines methods that random number generators implement, and this trait must be in scope for us to use those methods. The rand::thread_rng function will give us the particular random number generator that we’re going to use: one that is local to the current thread of execution and seeded by the operating system. Then we call the gen_range method on the random number generator. This method is defined by the Rng trait that we brought into scope with the use rand::Rng statement. The gen_range method takes a range expression as an argument and generates a random number in the range. The kind of range expression we’re using here takes the form start..end. It’s inclusive on the lower bound but exclusive on the upper bound, so we need to specify 1..101 to request a number between 1 and 100. Alternatively, we could pass the range 1..=100, which is equivalent. 
Have a look at rust std crate documentation [https://docs.rs/rustc-std-workspace-std/1.0.1/std/](https://docs.rs/rustc-std-workspace-std/1.0.1/std/)

### A Tour of The Rust Standard Library
[http://web.mit.edu/rust-lang_v1.25/arch/amd64_ubuntu1404/share/doc/rust/html/std/index.html](http://web.mit.edu/rust-lang_v1.25/arch/amd64_ubuntu1404/share/doc/rust/html/std/index.html)

### Very informative Rust Beginners book
[https://stevedonovan.github.io/rust-gentle-intro/object-orientation.html](https://stevedonovan.github.io/rust-gentle-intro/object-orientation.html)

### Comparing Number 
```rust
use rand::Rng;
use std::cmp::Ordering;
use std::io;

fn main() {
    // --snip--

    println!("You guessed: {}", guess);

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
}
```
Rust has a strong, static type system. However, it also has type inference
Rust is a statically and strongly typed systems programming language. statically means that all types are known at compile-time, strongly means that these types are designed to make it harder to write incorrect programs.

### Shadowing
Shadowing is different from marking a variable as mut, because we’ll get a compile-time error if we accidentally try to reassign to this variable without using the let keyword. By using let, we can perform a few transformations on a value but have the variable be immutable after those transformations have been completed.

The other difference between mut and shadowing is that because we’re effectively creating a new variable when we use the let keyword again, we can change the type of the value but reuse the same name. For example, say our program asks a user to show how many spaces they want between some text by inputting space characters, but we really want to store that input as a number:
Rust is a statically typed language, which means that it must know the types of all variables at compile time.

---

### Data types.

#### Scalar Types
A scalar type represents a single value. Rust has four primary scalar types: integers, floating-point numbers, Booleans, and characters. 

#### Compound Types
Compound types can group multiple values into one type. Rust has two primitive compound types: tuples and arrays.

#### The Tuple Type
A tuple is a general way of grouping together a number of values with a variety of types into one compound type. Tuples have a fixed length: once declared, they cannot grow or shrink in size.

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```
To extract tuple values
```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {}", y);
}
```
We can access a tuple element directly by using a period (.)
```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```
#### The Array Type
Another way to have a collection of multiple values is with an array. Unlike a tuple, every element of an array must have the same type. Arrays in Rust are different from arrays in some other languages because arrays in Rust have a fixed length, like tuples.

```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
    //or
    let a: [i32; 5] = [1, 2, 3, 4, 5];
}
```
An array isn’t as flexible as the vector type, though. A vector is a similar collection type provided by the standard library that is allowed to grow or shrink in size. 
> Array are stack allocated and can not grow or shrink, where as a vector is heap allocated and thus can grow or shrink.
An example of when you might want to use an array rather than a vector is in a program that needs to know the names of the months of the year. It’s very unlikely that such a program will need to add or remove months, so you can use an array because you know it will always contain 12 elements.

#### Accessing Array Elements
```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```
If we provide wrong index to an array that will be a **run time error**
---
## Functions
Function bodies are made up of a series of statements optionally ending in an expression. 
- Statements are instructions that perform some action and do not return a value. 
- Expressions evaluate to a resulting value.
- Function definitions are also statements.
Statements do not return values. Therefore, you can’t assign a let statement to another variable, as the following code tries to do; you’ll get an error. The let y = 6 statement does not return a value, so there isn’t anything for x to bind to. This is different from what happens in other languages, such as C and Ruby, where the assignment returns the value of the assignment. In those languages, you can write x = y = 6 and have both x and y have the value 6; that is not the case in Rust.

```rust
fn main() {
    let x = (let y = 6);
}
```
Expressions evaluate to something and make up most of the rest of the code that you’ll write in Rust. Consider a simple math operation, such as 5 + 6, which is an expression that evaluates to the value 11.Expressions can be part of statements
Calling a function is an expression. Calling a macro is an expression. The block that we use to create new scopes, {}, is an expression
```rust
fn main() {
    let x = 5;

    let y = {
        let x = 3;
        x + 1
    };

    println!("The value of y is: {}", y);
}
```
>  In Rust, the return value of the function is synonymous with the value of the final expression in the block of the body of a function. You can return early from a function by using the return keyword and specifying a value, but most functions return the last expression implicitly.

```rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {}", x);
}
```

- There are no function calls, macros, or even let statements in the five function—just the number 5 by itself. That’s a perfectly valid function in Rust. Note that the function’s return type is specified too, as -> i32. 
---
### OOP in Rust
The relationships between various data types in Rust are established using traits. **A large part of learning Rust is understanding how the standard library traits operate**, because that's the web of meaning that glues all the data types together.

*Traits are interesting because there's no one-to-one correspondence between them and concepts from mainstream languages*. It depends if 

So Rust traits allow traditional polymorphic OOP. But what about inheritance? People usually mean implementation inheritance whereas Rust does interface inheritance.

Implementation inheritance has some serious problems. But it does feel so very convenient. There's this fat base class called Animal and it has loads of useful functionality (it may even expose its innards!) which our derived class Cat can use. That is, it is a form of code reuse. But code reuse is a separate concern.

Getting the distinction between implementation and interface inheritance is important when understanding Rust.

Note that traits may have provided methods. Consider Iterator - you only have to override next, but get a whole host of methods free. This is similar to 'default' methods of modern Java interfaces. Here we only define name and upper_case is defined for us. We could override upper_case as well, but it isn't required.

> In rust vectors and arrays can only have one data type, there can not be an array or vector of strings and int. Further more vectors can grow and shrink where as arrays dont. A struct on the other hand is used to mix and match different data types and thus contain any number of arrays and vectors.
---
### Traits as Parameters, and the Trait Bound Syntax 
At this point, you might be asking - “Why is this useful? I mean, why don’t we just drop the trait bits and just declare this method under a regular old impl Person block?”

As alluded to at the end of the previous section, the primary reason we focus on defining and then implementing certain behavior, is that we can then build APIs that are behavior-centric, and not just type-centric. Rather than building functions that only accept a certain, predefined type, we can build functions that instead allow any type to be passed in, provided they implement a certain behavior, or set of behaviors. In other words, you can use Traits in the place of concrete types, such as in function parameters.

