# Creating File
Creating a Simple file.
```rust
use std::io::Write;
fn main() {
    lw file_name = "test_doc.txt";
    let mut my_file = std::fs::File::create("test_doc.txt").expect("creation failed");
    my_file.write_all("This is the first message".as_bytes()).expect("write failed");
    my_file.write_all(" Keep working".as_bytes()).expect("write failed");
    println!("The tag line of Chercher.tech has been added, open the file to see :)");

    //========== Now lets read the same file
    let mut f = File::open("foo.txt")?;
     let mut buffer = [0; 10];
    // read up to 10 bytes
    let n = f.read(&mut buffer)?;
    println!("The bytes: {:?}", &buffer[..n]);
}
```
