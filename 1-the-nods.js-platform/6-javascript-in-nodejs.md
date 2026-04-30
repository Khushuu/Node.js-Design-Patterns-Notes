# JavaScript in Node.js

JavaScript in Node.js is different from browser JavaScript.

In the browser, JavaScript runs in a secure environment with no direct access to the system.

In Node.js, JavaScript can access the filesystem, network, databases, and more.

This means Node.js does not have a DOM, and there is no `window` or `document` object.

## Running Modern JavaScript

Browsers need to support many devices and versions. Old browsers may not understand new JavaScript features.

Node.js usually runs on known systems and known runtime versions.

That means we can use newer ECMAScript features more safely in Node.js without transpilers.

If you build a library for others, you may still target the oldest active Node.js LTS version.

Use `engines` in `package.json` to warn users about incompatible Node.js versions.

Important links:
- Node.js release cycles: nodejsdp.link/node-releases
- `package.json` engines: nodejsdp.link/package-engines
- ES support by Node.js version: nodejsdp.link/node-green

## Module System

Node.js started with **CommonJS**, using `require` to import built-in modules or files.

CommonJS helped JavaScript applications become large and well organized.

Browsers later gained ES modules with `import`, but Node.js still handles local files differently from browsers.

We will discuss Node.js modules in more detail later.

## Full Access to Operating System Services

Node.js can use many OS features through built-in modules:
- `fs` for filesystem access
- `net` and `dgram` for TCP/UDP sockets
- `http` and `https` for servers
- `crypto` for encryption and hashing
- `v8` for V8 internals
- `vm` for V8 contexts
- `child_process` for running other processes
- `process` for environment variables and CLI arguments

For a full reference, see: nodejsdp.link/node-docs
