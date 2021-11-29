# Struct Printing
```rust
#[derive(Debug)]    
struct Point {
    x:i32,
    y:i32,
}
fn main(){

let pt = Point {
    x:44, 
    y:66}; 

println!("{:?}",pt);
}//--main
```