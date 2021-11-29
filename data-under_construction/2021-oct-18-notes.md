## Notes
The problem with inheretence is that the complexity increase exponenetially.
In Rust the emphasis is on composition and not inheretance. Code reuse is made sure using composition and not inheretance.
Traits are a way to share behaviour between different different structs/?. 
In my experience, default implementations are most useful when I am creating the trait and the types that use that trait’s implementation. This is a way of reducing unnecessarily duplicated code, primarily. The vast majority of the times I’ve seen traits as part of an external crate’s (library) API, it required me to provide implementations for them, as a way of forcing me to really define how I expect that behavior to be expressed in my codebase.
[https://oswalt.dev/2020/07/rust-traits-defining-behavior/](https://oswalt.dev/2020/07/rust-traits-defining-behavior/)

> Trait can also be returned from a function. It means that the trait (the behaviour) can be decided at run time. This changes everything.
