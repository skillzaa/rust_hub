# Vertors in Rust Part3
Following topics are intended to be covered
1. creating vector
2. Referencing items 
5. Iterating over vec, three ways.
3. Extract a vector out of another vector (using filters and collect).


## Creating a vector
Basically has two  methods
```rust
let x = vec![1,2,3,4,5];
let y:Vec<i32> = Vec::new();
```
## Referencing a vector items
Basically has two  methods
```rust
 let third: &i32 = &v[2]; //=====> strange but often used
 //and  
 let x = v.get(2) //===> will return Option
``` 
## Iterating over vec
```rust
let mut v = vec![1, 2, 3, 4, 5];

for i in &v {
    println!("A reference to {}", i);
}

for i in &mut v {
    println!("A mutable reference to {}", i);
}

for i in v {
    println!("Take ownership of the vector and its element {}", i);
}
```

## Using Filters
We can extract a vector out of another vector using filter and collect.
```rust
let numbers: Vec<i32> = vec![
  1, 2, 3, 4, 5, 6, 7, 8, 9, 10,
];

let even_numbers = numbers
  .into_iter()
  .filter(|n| n % 2 == 0)
  .collect::<Vec<_>>();

println!("{:?}", even_numbers);
```
### Future Projects
1. check if a vec has some items of another vector (overlap).
1. check if a vec has some items of another vector (superset).
1. check if a vec is subset of another vec (subset).
1. sort a vec.
1. comparing two vectors.
