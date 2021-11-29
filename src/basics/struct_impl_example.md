# Struct Impl Example
```rust
#[derive(Debug)]

struct Rectangle {
    width:u32,
    height:u32,
}

impl Rectangle {
    fn area(&self)-> u32{
        self.width * self.height
    }
}

fn main(){

let rect = Rectangle {
    width:55,
    height:80,
};

println!("The area is :: {}", rect.area());

}//--main
```