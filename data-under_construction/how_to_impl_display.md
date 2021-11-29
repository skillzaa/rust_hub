# How To Implement Display Trait

```rust
use std::fmt;

// Debug can be auto-generated
#[derive(Debug)]
struct MyType {
    x: u32,
    y: u32
}

// but not Display
impl fmt::Display for MyType {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "x={},y={}", self.x, self.y)
    }
}

let t = MyType{x:1,y:2};
println!("{}", t); //=> x=1,y=2
println!("{:?}", t); //=> MyType { x: 1, y: 2 }
```