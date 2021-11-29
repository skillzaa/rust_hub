# Duration Between Two Points of Time
```rust
use std::time::SystemTime;
fn main() {

    let sys_time = SystemTime::now();
    // println!("{:?}",sys_time.tv_sec);
    let new_sys_time = SystemTime::now();
    let difference = new_sys_time.duration_since(sys_time)
        .expect("Clock may have gone backwards");
    println!("{:?}", difference);
}
```