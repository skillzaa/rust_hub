# Serde json
This is an example of Serde serializing and deserializing vector of structs.

```rust
use std::fs::File;
use std::io::Write;
use serde::{Deserialize, Serialize};
use serde_json::Result;

#[derive(Serialize, Deserialize)]
#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
}

fn main() -> Result<()> {
    deserialize()?;
    serialize()?;
   Ok(())
}
//========================
fn deserialize()->Result<()>{
     // Some JSON input data as a &str. Maybe this comes from the user.
     let data = r#"
     [{
         "name": "John Doe",
         "age": 43
     },
     {
        "name": "Jane Michels",
        "age": 35
    }]
     "#;
 let pers: Vec<Person> = serde_json::from_str(data)?;
 println!("Pers {:?}", pers);

 Ok(())
}
fn serialize()->Result<()>{
    let mut j : Vec<Person> = Vec::new();
    j.push(Person { name: String::from("jill"), age: 96 });
    j.push(Person { name: String::from("mike"), age: 11 });
    j.push(Person { name: String::from("nikey"), age: 33 });

    let pers:String = serde_json::to_string(&j)?;
    println!("serialize {}",pers);
    Ok(())
}

```