# WasmDemo

This repository is a tryout for a video tutorial: [What is WebAssembly? And what's it got to do with Docker? | WASM vs Docker | KodeKloud](https://www.youtube.com/watch?v=7553XZ0T6pM).

## Requirements

You need to [install and setup Emscripten](https://emscripten.org/docs/getting_started/downloads.html) to run `emcc` command(`.wasm` file builder).

## How to build

***You **cannot** use output .wasm file for different environment(e.g. a file output for node.js won't run on Docker).***

### For browsers

Run for C:

```sh
emcc helloworld.c -o helloworld.html
```

Run for C++:

```sh
em++ helloworld.cpp -o helloworld.html
```

Then access `./helloworld.html` from local web server.

### For node.js

Run:

```sh
emcc helloworld.c -o helloworld.js
```

Then you can run:

```sh
node helloworld.js
```

(Obviously, you need node runtime.)

### For Docker

Build WASM file:

```sh
emcc helloworld.c -o helloworld.wasm
```

Build image:

```sh
docker buildx build --platform wasi/wasm32 -t kodekloud/wasm-docker-hello-1 .
```

Run container:

```sh
docker run --rm --name=wasm-docker-c-program --runtime=io.containerd.wasmedge.v1 --platform=wasi/wasm32 kodekloud/wasm-docker-hello-1:latest
```

## What's left to do

Contain `.wasm` file build process like [this](https://github.com/mikesir87/wasm-example/blob/main/Dockerfile).
