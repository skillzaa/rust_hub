# Some None Example
```rust
#[derive(Debug)]
struct Obj {
no:u128,
id:u128,
}

impl Obj{
   fn new(no:u128,id:u128)->Obj{
      Obj {
         no:no,
         id:id,
      }
   }
}         

fn main (){
let mut v:Vec<Obj> = Vec::new();
v.push(Obj::new(44, 68));

//-- lets get some here
match v.get(0) {
                  Some(x)=> println!("{:?}--Result is success i.e Some",x.no),
                  None => println!("--Result is failure i.e None")
}

match v.get(20) {
                  Some(x)=> println!("{:?}--Result is success i.e Some",x.no),
                  None => println!("--Result is failure i.e None")
} 

println!("{:?}",v.get(20));

}
```
