# The Revealing Module Pattern

- Revealing module pattern is a foundational JavaScript pattern.
- It provides information hiding and helps build a primitive module system.
- It is useful to understand how ES modules and CommonJS work internally.
- It solves the global scope problem by creating a private scope.
- It exposes only the public API while keeping internals private.

## Example
```js
const myModule = (() => {
  const privateFoo = () => {}
  const privateBar = []

  console.log('Inside:', privateFoo, privateBar)

  const exported = {
    publicFoo: () => {},
    publicBar: () => {},
  }

  return exported
})()

console.log('Outside:', myModule.privateFoo, myModule.privateBar)
console.log('Module:', myModule)
```

- The IIFE creates a private scope.
- `privateFoo` and `privateBar` remain hidden from the outside.
- `myModule` only contains the exported API.
- Accessing `myModule.privateFoo` or `myModule.privateBar` returns `undefined`.

## What this teaches us
- Modules are the bricks for structuring applications.
- They enforce private implementation details.
- The revealing module pattern is a simple precursor to CommonJS.
- It shows how export behavior can be implemented without a module loader.
