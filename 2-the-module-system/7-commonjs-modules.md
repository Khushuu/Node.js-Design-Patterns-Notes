# CommonJS Modules

- CommonJS is still widely used in legacy Node.js code.
- New projects are recommended to use ES modules.
- CommonJS is not deprecated.

## Core concepts
- `require()` imports modules.
- `exports` and `module.exports` export functionality.
- `require()` is synchronous and dynamic.

## Example
```js
// math.cjs
'use strict'
function add(a, b) {
  return a + b
}
module.exports = { add }

// main.cjs
'use strict'
const { add } = require('./math.cjs')
console.log(add(2, 3)) // 5
```

## Important details
- CommonJS does not run in strict mode by default.
- `require()` resolves, loads, and executes the module immediately.
- This makes initialization predictable.
- This also makes module loading less flexible than ESM.

## Dynamic require
- `require()` can be used inside functions, conditionals, or loops.
- This supports runtime decisions.
- It complicates dependency analysis.

## Asynchronous initialization
- CommonJS modules are loaded synchronously.
- Asynchronous module setup is possible but not immediate.
- This can make module readiness harder to guarantee.

## Historical note
- Node.js removed the asynchronous version of `require()` early on.
- The reason: async `require()` made initialization more complex.
