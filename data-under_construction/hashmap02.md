# Hash Map - Part 2
```rust
fn main(){
    use std::collections::HashMap;
    #[derive(Hash, Eq, PartialEq, Debug)]
        struct Viking {
            name: String,
            country: String,
        }
        
        impl Viking {
            /// Creates a new Viking.
            fn new(name: &str, country: &str) -> Viking {
                Viking { name: name.to_string(), country: country.to_string() }
            }
        }
        
        // Use a HashMap to store the vikings' health points.
        let mut vikings:HashMap<Viking,u32>= HashMap::new();
        
        vikings.insert(Viking::new("Einar", "Norway"), 25);
        vikings.insert(Viking::new("Olaf", "Denmark"), 24);
        vikings.insert(Viking::new("Harald", "Iceland"), 12);
        
        // Use derived implementation to print the status of the vikings.
        for (viking, health) in &vikings {
            println!("{:?} has {} hp", viking, health);
        }
        println!("--------------------");
    
        for (key, value) in vikings.into_iter() {
            println!("{:?} = {}", key, value);
            //This line will cause error : safety
            // vikings.remove(key);
        }
    }
```    