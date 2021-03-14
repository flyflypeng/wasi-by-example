# WASI Hello World Example README

## Build Steps

```bash
$ rustup target add wasm32-wasi
$ cd wasi_hello_world
$ cargo build --target wasm32-wasi
```

Our wasm file should be compiled to target/wasm32-wasi/debug/wasi_hello_world.wasm. And now we can actually run our program!

```bash
$ ls target/wasm32-wasi/debug/
target/wasm32-wasi/debug                                                                                                                                               
build                 deps                  examples              incremental           wasi_hello_world.d    wasi_hello_world.wasm
```

## Running WASM module with wasmer

We choose the AOT method to run the WASM module.

1. compile the wasm module to ELF format shared object

```bash
$  wasmer compile --cranelift --native wasi_hello_world.wasm -o wasi_hello_world.so
Engine: native
Compiler: cranelift
Target: x86_64-unknown-linux-gnu
✔ File compiled successfully to `wasi_hello_world.so`
```

2. run the ELF shared object with wasmer run command

```bash
$ wasmer run ./wasi_hello_world.so --mapdir /helloworld:.
Hello world!

$ cat ./helloworld.txt
Hello world!
```
