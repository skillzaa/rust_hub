### My understanding of multi media programming as of 21-oct-2021

I spent few hours of reading about multi media programming and found following

1. The old technology (industry standerd) was **OpenGl** and that still stays but is slowly dieing.
1. OpenGl was extended to be usable in web space as **WebGl**.
1. OpenGl as well as WebGl both suffered from many problems and there was a need for a new API.
1. **Vulcan** is the new low level API. It is the new thing and is very fast as compared to OpenGl. It provides a lot of power to the user but at the same time it is more complex and more low level than OpenGl.
1. I think vulcan make use of GPU for processing.
1. **vulkano** is the rust wrapper crate for Vulcan.
1. Just like WebGl was the web implementation of OpenGl similarly **WebGPU is the web implementation of Vulcan**. So WebGPU is the future of web graphics but is still under experimental flag.
---
## Conclusion
1. For the time being material and tutorials on the Vulcan as well as WebGPU are very less.
1. It will NOT be a bad idea to try WebGl for a while since its available every where and is not being depricated anytime soon. Also the study material may be available a lot. also the basic techniques are the same.
1. You must learn Rust and then Webassembly first for that.  