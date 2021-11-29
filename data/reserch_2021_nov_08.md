## Reserch

Functionality-wise, stdweb is an all-in-one-solution roughly equivalent to wasm_bindgen + web-sys + js-sys. 

wasm-bindgen definitely has more long term potential as it's officially supported by the Rust team not stdweb

js-sys and web-sys aim to be the libc of JavaScript and the Web respectively, 

stdweb has low development speed

Rust **Hyper** is the base framework for rocket and almost all other frameworks. The ActiX uses Tokio.

The big thing is that js-sys and web-sys are built on top of wasm-bindgen. wasm-bindgen has been designed and built with an eye towards leveraging the "host bindings" proposal to eventually get even-faster-than-JS DOM performance, because DOM calls can be validated at wasm compile time rather than dynamically type checked on every call.

wasm-bindgen's other focus is to enable you to only pay for what you use. If you only use js_sys::Array::new and js_sys::Array::push, then you won't entrench bindings to js_sys::Object::freeze in your binary.

js-sys and web-sys are meant to be libc-style crates that just provide the raw bindings and building blocks. We want to get this layer rock solid so that no one else has to put in the effort to do the same, and can instead focus on higher level abstractions and libraries.


I think the web-sys/js-sys should be seen as a kind of libc for the web, low level and complete, and wasm-bindgen as something that integrates into the rust build system, with just a single binary to run to generate your rust and js.



wasm-bindgen facilitates communication between JavaScript and Rust compiled to WebAssembly. It allows you to speak in terms of Rust structs, JavaScript classes, strings, etc… instead of only the integers and floats supported by WebAssembly’s raw calling convention. You only pay for what you use,

