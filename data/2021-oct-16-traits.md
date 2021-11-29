# 2021-oct-16 Traits in Rust
### Definition
> A trait is a collection of methods defined for an unknown type: Self. They can access other methods declared in the same trait.Traits can be implemented for any data type.
---
> A trait tells the Rust compiler about functionality a particular type has and can share with other types.We can use traits to define shared behavior in an abstract way.
---
> Traits are similar to a feature often called interfaces in other languages, although with some differences.
---
- When an object implements a trait it has to provide implementation for those methods for which default implementation is not provided. For methods which default implementation is provided can be over written or accepted.
---
> A type’s behavior consists of the methods we can call on that type. Different types share the same behavior if we can call the same methods on all of those types. Trait definitions are a way to group method signatures together to define a set of behaviors necessary to accomplish some purpose.
---
- Before using a trait we need to bring the trait into scope first.*Which means that this trait needs to be public in its own defined crate.
- One restriction to note with trait implementations is that we can implement a trait on a type only if either the trait or the type is local to our crate (means declared in that craten).We can’t implement external traits on external types  
#### What is Dynamic Dispatch
In computer science, dynamic dispatch is the process of selecting which implementation of a polymorphic operation (method or function) to call at run time. It is commonly employed in, and considered a prime characteristic of, object-oriented programming (OOP) languages and systems.
**Polymorphism is the phenomenon wherein somewhat interchangeable objects each expose an operation of the same name but possibly differing in behavior**
OR
**polymorphism gives us the ability to present a single interface for potentially many different concrete types. This allows us to create more flexible APIs which give more control to the consumer and are easier to maintain.There are several practical advantages to using polymorphism, but one of the biggest is code re-use. If you design an API around specific, concrete types, then you’re committed to that approach, and so are your consumers.**
- We should keep the behaviour seperate from data so that it is flexable.
- Polymorphism allows us to create functions that accept any type, as long as those types exhibit certain behaviors or properties that we need them to have.
<br/>
<img src="./images/polymorphism.png">
In this case, that behavior is actually all we care about, so we can leverage polymorphism to be more flexible, but maintain a set of required functionality. Through this, we can do things like write a single function that accepts multiple types.
[credit](https://oswalt.dev/2021/06/polymorphism-in-rust/)
This is the general idea behind why we would want to use polymorphism in any language, but what options for polymorphism exist in Rust? There are two primary ways, and both of these have trade-offs to consider when it comes to performance as well as binary size:

**Static Dispatch** 
- this approach leverages generics (also called parametric polymorphism) and (usually) trait bounds to provide the flexibility we need while still maintaining full type safety, and without requiring a lot of duplicate code. This approach is extremely performant (in Rust this is known as a “zero-cost abstraction”) - however, due to monomorphization, this does create a larger binary size.

**Dynamic Dispatch** 
- this approach uses “trait objects” to punt the decision of which type is required to satisfy some kind of polymorphic interface to runtime. This cuts down on binary size (as no monomorphization is used here) but incurs a performance penalty due to the extra lookup at runtime. This approach also explicitly forbids the use of generics.
- Dynamic dispatch can be characterized as the opposite of static dispatch. Where static dispatch choses to create copies of all functions that use generic parameters and store these in the binary, dynamic dispatch choses to store only a single copy, but then calculates the necessary concrete implementation at runtime.
- In Rust, dynamic dispatch leverages “Trait Objects” to achieve polymorphism. Unlike trait bounds, which is an optional constraint you can add to generic parameters, trait objects actually cannot be used with generics at all, and instead are the required method for performing dynamic dispatch in Rust.The syntax for trait objects these days is characterized by the dyn keyword, followed by the name of a Trait
- The dyn keyword was introduced in Rust 1.27 and is now the idiomatic way to explicitly specify that you wish to use dynamic dispatch through trait object.
- Even though we’re not using generic parameters, the compiler still needs a little help to know the size of our types at compile-time. This is why you’ll commonly see trait bounds passed in via reference.
```rust
fn dynamic_dispatch(t: &dyn Growler) {
    t.growl();
}
```
---
### Traits as Parameters (trait bounds)
*When we want to base our code on behaviour and not data type we specify a trait as an argument to a function* (and not a data type). In this way we can give this function any data type as long as that data type implements that trait.
We normally create a Vector and wrap it in **Box** with **dyn** key word. 

### Trait Object
 A trait object points to both an instance of a type implementing our specified trait as well as a table used to look up trait methods on that type at runtime But trait objects differ from traditional objects in that we can’t add data to a trait object. Trait objects aren’t as generally useful as objects in other languages: their specific purpose is to allow abstraction across common behavior.
 > Trait objects are more like objects in other languages in the sense that they combine data and behavior.
 We create a trait object by specifying some sort of pointer, such as a & reference or a Box<T> smart pointer, then the dyn keyword, and then specifying the relevant trait. Trait objects must use a pointer.
 - Trait objects can be thought of like objects of an Interface Type in Java, defining common functionality for the Types implementing them. When using a trait object, we don’t care what exact type is used, we just make sure that given functionality is present.
---
> ‘Monomorphization’ a fancy term for saying the compiler fills in the concrete types for the generic ones at compile time and duplicates the code if necessary. 
---
### Conclusion
- We use trait bounds (Traits as Parameters) with static dispatch along with generics. We get a seperate fn for each type at compile time.
- We use trait objects for dynamic dispatch. In this we use the **dyn** keyword and we do not use generics. A **v table** is used. 
---
---
