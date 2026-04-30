# libuv and the Internal Components of Node.js

## What is libuv?

Each operating system has its own event interface: epoll on Linux, kqueue on macOS, IOCP on Windows.

libuv is a native library that hides these differences and gives Node.js a common I/O layer.

It also implements the reactor pattern for Node.js.

libuv is the low-level I/O engine of Node.js. It provides:
- event loops
- event queues
- asynchronous I/O operations
- task queuing

## The Complete Recipe for Node.js

Node.js depends on three main parts:
- **Bindings** that wrap libuv and other low-level APIs for JavaScript.
- **V8**, the JavaScript engine from Google.
- A **core JavaScript library** that exposes the high-level Node.js API.

Together, these components form the Node.js runtime.
