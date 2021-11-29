# Reading File
It is as simple as that, even simpler than Javascript and PHP.

```rust
use std::fs;
fn main() {
    let file_name = "test_doc.txt";
    let content = fs::read_to_string(file_name).unwrap();
    for line in content.lines() {
        println!("{}", line);
    }
}
```
