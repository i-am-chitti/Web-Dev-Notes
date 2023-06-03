# WebAssembly

WebAssembly is a new type of code that can be run in modern web browsers and provides new features and major gains in performance. It is not primarily intended to be written by hand, rather it is designed to be an effective compilation target for source languages like C, C++, Rust, etc.

This has huge implications for the web platform — it provides a way to run code written in multiple languages on the web at near-native speed, with client apps running on the web that previously couldn't have done so.

What's more, you don't even have to know how to create WebAssembly code to take advantage of it. WebAssembly modules can be imported into a web (or Node.js) app, exposing WebAssembly functions for use via JavaScript. JavaScript frameworks could make use of WebAssembly to confer massive performance advantages and new features while still making functionality easily available to web developers.

### Web Assembly Goals

- Be fast, efficient, and portable — WebAssembly code can be executed at near-native speed across different platforms by taking advantage of common hardware capabilities.
- Be readable and debuggable — WebAssembly is a low-level assembly language, but it does have a human-readable text format (the specification for which is still being finalized) that allows code to be written, viewed, and debugged by hand.
- Keep secure — WebAssembly is specified to be run in a safe, sandboxed execution environment. Like other web code, it will enforce the browser's same-origin and permissions policies.
- Don't break the web — WebAssembly is designed so that it plays nicely with other web technologies and maintains backwards compatibility.


### How does WebAssembly fit into the Web?

A Web platform consists of two parts

1. A VM is what does JIT compilation of the application's code.
2. Core Web APIS that the Web app can call to control web browser/device functionality and make things happen

Historically, the VM has been able to load only JavaScript. This has worked well for us as JavaScript is powerful enough to solve most problems people have on the Web today. We have run into performance problems, however, when trying to use JavaScript for more intensive use cases like 3D games, Virtual and Augmented Reality, computer vision, image/video editing, and a number of other domains that __demand native performance__

Additionally, the cost of downloading, parsing, and compiling very large JavaScript applications can be prohibitive. Mobile and other resource-constrained platforms can further amplify these performance bottlenecks.

#### Difference between WebAssembly and Javascript

- JavaScript is a high-level language, flexible and expressive enough to write web applications. It has many advantages — it is dynamically typed, requires no compile step, and has a huge ecosystem that provides powerful frameworks, libraries, and other tools.

- WebAssembly is a low-level assembly-like language with a compact binary format that runs with near-native performance and provides languages with low-level memory models such as C++ and Rust with a compilation target so that they can run on the web.

With the advent of WebAssembly appearing in browsers, the virtual machine that we talked about earlier will now load and run two types of code — JavaScript AND WebAssembly.

The different code types can call each other as required — the WebAssembly JavaScript API wraps exported WebAssembly code with JavaScript functions that can be called normally, and WebAssembly code can import and synchronously call normal JavaScript functions. In fact, the basic unit of WebAssembly code is called a module and WebAssembly modules are symmetric in many ways to ES modules.

## Key Concepts

Following -

1. Module: Represents a WebAssembly binary that has been compiled by the browser into executable machine code. A Module is stateless and thus, like a Blob, can be explicitly shared between windows and workers (via postMessage()). A Module declares imports and exports just like an ES module.
2. Memory: A resizable ArrayBuffer that contains the linear array of bytes read and written by WebAssembly's low-level memory access instructions.
3. Table: A resizable typed array of references (e.g. to functions) that could not otherwise be stored as raw bytes in Memory (for safety and portability reasons).
4. Instance: A Module paired with all the state it uses at runtime including a Memory, Table, and set of imported values. An Instance is like an ES module that has been loaded into a particular global with a particular set of imports.

The JavaScript API provides developers with the ability to create modules, memories, tables, and instances. Given a WebAssembly instance, JavaScript code can synchronously call its exports, which are exposed as normal JavaScript functions. Arbitrary JavaScript functions can also be synchronously called by WebAssembly code by passing in those JavaScript functions as the imports to a WebAssembly instance.

Since JavaScript has complete control over how WebAssembly code is downloaded, compiled and run, JavaScript developers could even think of WebAssembly as just a JavaScript feature for efficiently generating high-performance functions.

In the future, WebAssembly modules will be loadable just like ES modules (`using <script type='module'>)`, meaning that JavaScript will be able to fetch, compile, and import a WebAssembly module as easily as an ES module.


## How to use it?

The WebAssembly ecosystem is at a nascent stage; more tools will undoubtedly emerge going forward. Right now, there are four main entry points:

- Porting a C/C++ application with Emscripten.
- Writing or generating WebAssembly directly at the assembly level.
- Writing a Rust application and targeting WebAssembly as its output.
- Using AssemblyScript which looks similar to TypeScript and compiles to WebAssembly binary.

The WebAssembly specification details two file formats, a binary format called a WebAssembly Module with a .wasm extension and corresponding text representation called WebAssembly Text format with a .wat extension.

WebAssembly modules cannot directly access OS functionality on its own. A third-party tool Wasmtime can be used to access this functionality. Wasmtime utilizes the WASI API to access the OS functionality.


## Resources

- [Understanding WebAssembly Text Format](https://developer.mozilla.org/en-US/docs/WebAssembly/Understanding_the_text_format)

-
