# Reading Directory

```rust
use std::fs;


fn main() {

for entry in fs::read_dir(".").unwrap() {
  let entry = entry.unwrap();
  let path = entry.path();
  if path.is_dir() {
      println!("{:?} is a dir", path);
  } else {
      println!("{:?} is a file", path);
  }
}

}//main

```