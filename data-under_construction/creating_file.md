# Creating File
================
Creating a Simple file.

```rust
use std::fs::File;
use std::io::Write;
fn main() {
    let file_name = "test_doc.txt";
    let mut my_file = File::create(file_name).expect("creation failed");
    my_file.write_all("This is the first message".as_bytes()).expect("write failed");
    my_file.write_all(" Keep working".as_bytes()).expect("write failed");
    println!("The file has been created and text has been added:)");
}
```
