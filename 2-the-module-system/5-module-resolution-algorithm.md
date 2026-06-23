# Module Resolution Algorithm

- Dependency hell: when dependencies require incompatible versions of the same library.
- Node.js solves this by resolving modules based on the importer location.
- The algorithm maps a module specifier to a filesystem file or core module.

## Module identifiers
- `./logger.js` and `../logger.js` are relative specifiers.
- `/opt/nodejs/config.js` and `file:///opt/nodejs/config.js` are absolute specifiers.
- `http` and `fastify` are bare specifiers.
- `node:http` is the preferred core module prefix.
- `fastify/lib/logger.js` is a deep import specifier.

## Resolution branches
- File modules:
  - `/...` => absolute file path.
  - `./...` or `../...` => relative path from the importing module.
- Core modules:
  - bare specifiers first check built-in Node.js modules.
  - `node:` prefix returns the same core module.
- Package modules:
  - search `node_modules` upward from the importing module.
  - the first matching package wins.

## import.meta.resolve examples
```js
console.log(import.meta.resolve('./utils/example.js'))
// -> file://<project_path>/utils/example.js

console.log(import.meta.resolve('assert'))
// -> node:assert

console.log(import.meta.resolve('node:assert'))
// -> node:assert

console.log(import.meta.resolve('fastify/lib/logger.js'))
// -> file://<project_path>/node_modules/fastify/lib/logger.js
```

## Private dependency example
- `myApp/foo.js` imports `depA` => `/myApp/node_modules/depA/index.js`
- `depB/bar.js` imports `depA` => `/myApp/node_modules/depB/node_modules/depA/index.js`
- `depC/foobar.js` imports `depA` => `/myApp/node_modules/depC/node_modules/depA/index.js`
- Each package can keep its own private dependency version.

## Key takeaway
- Resolution is the core of Node.js dependency management.
- It prevents collisions by isolating dependencies per importer.
