# Struct Impl Example-2
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
    fn can_hold(&self,other:&Rectangle)->bool{
        self.width > other.width && self.height > other.height
    }
}
//-------This is the second impl block for associative function (a static function). This does not take &self rather take on other values.
impl Rectangle {
    fn square(size:u32)->Rectangle {
        Rectangle {
            width:size,
            height:size,
        }
    }
}
fn main(){
let rect01 = Rectangle {
    width:55,
    height:80,
};
let rect02 = Rectangle {
    width:22,
    height:10,
};
let rect03 = Rectangle {
    width:2,
    height:8,
};

println!("The area is :: {}", rect01.area());
println!("Can rect01 hold rect02 (hint:true)? {}", rect01.can_hold(&rect02));
println!("Can rect01 hold rect03 (hint:true)? {}", rect01.can_hold(&rect03));
println!("Can rect02 hold rect01 (hint:false)? {}", rect02.can_hold(&rect01));
println!("Can rect03 hold rect01 (hint:false)? {}", rect03.can_hold(&rect01));
//----------------------------------------------
//----------------------------------------------
println!("The associated/static fn :Rectangle::square(88):: {:?}", Rectangle::square(88));

}//--main
```