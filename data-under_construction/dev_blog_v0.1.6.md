
## Development Blog
2021-11-08

### Wrap , Result and Main fn
The main fn must never have unwrap. It is sinful.
All the Result<> should bubble upto main where they are presented as one match statement. You actually need just one match statement at the top level in the main function if that is what you want.
At mid levels if there is an error (from code at lower level) the mid level fn always has an option to use ? and let it bubble up to the main fn at top.
Every process that ends in main (by the way all processes start and end in main) must have one top level match statement to manage the outcome from that process. Not having a Result and match statement at the end of a process is not logical.

At times we want to discard the result of a function returning a result or an option.

```
fn some_fn ()->Result<bool,Error>{
    Ok(true) 
}
 let _ = some_fn(); // Discarding Result
```

### Present Structure of the Application
At the moment Hulk has 3 layers.

1. **The Brown Library** : 
This is the core of the app, everything is built on top of this, it has to be 100% test covered.
The library is flat which means that there is no abstraction built at this level. There are internal fn calls but all that is just to break the work and not for abstractions. Most of the functions are just wrappers around Rust fn. 
All in all it just gives a great interface to deal with Rust file system, which is exectly its task.

2. **controllers** : 
This is where abstraction happen. I want this to be just function calls to brown library and then stitching the results.

3. **The main function** :
As usual a place to stitch the app together.

### The Boring Work is the Actual Work

Once all the technical problems have been solved comes the boring work of putting it all together, but this is the actual work where the product gets polished.

### Folders With many modules
If one needs a folder where he can save a number of modules the simple solution is to still export all of the modules from mod.rs using **pub use**. 

### Items to add to Brown lib
- get_file_name -- from DirEntry
- get_file_ext -- from DirEntry
