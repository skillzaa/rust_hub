# Hash Map - Part 1
```rust
fn main(){
use std::collections::HashMap;
let mut hm:HashMap <String,u128> = HashMap::new();

hm.insert("one".to_string(),1);
hm.insert("two".to_string(),2);
hm.insert("three".to_string(),3);
hm.insert("four".to_string(),4);
hm.insert("five".to_string(),5);

for (key, value) in &hm {
    println!("{}: {}", key, value);
}



}
```