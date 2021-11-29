# If let
You can think of if let as syntax sugar for a match that runs code when the value matches one pattern and then ignores all other values.

This code:
```rust
  let config_max = Some(3u8);
    match config_max {
        Some(max) => println!("The maximum is configured to be {}", max),
        _ => (),
    }
```
Can be written as 
```rust
 let config_max = Some(3u8);
    if let Some(max) = config_max {
        println!("The maximum is configured to be {}", max);
    }
```    

We can include an else with an if let.


