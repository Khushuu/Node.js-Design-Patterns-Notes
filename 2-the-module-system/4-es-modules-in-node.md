# ES Modules in Node.js

- ES modules were introduced in ES2015 to provide an official module system.
- They aim to bridge browser and server module management.
- The syntax is simple and supports static imports, exports, and live bindings.
- ES modules also support cyclic dependencies and async loading.

## ES modules in Node.js
- Node.js treated `.js` as CommonJS by default.
- ES modules had to be explicitly enabled for backward compatibility.
- Without enabling ESM, `import` statements in `.js` files trigger a syntax error.

## Example error
```bash
node index.js
```

```
(node:69441) Warning: To load an ES module, set "type": "module"
index.js:1
import { someFeature } from './someModule.js'
^^^^^^
SyntaxError: Cannot use import statement outside a module
```

## Ways to enable ES modules
- Use `.mjs` extension.
- Add `"type": "module"` in `package.json`.
- Use `--experimental-default-type="module"`.
- Use `--experimental-detect-module`.

## Recommended approach
- Use `package.json` with `"type": "module"`.
- Keep `.js` extensions while using ES module syntax.

```json
{
  "name": "sample-esm-project",
  "version": "1.0.0",
  "main": "index.js",
  "type": "module"
}
```

## ES module syntax
- Everything is private by default.
- Only exported entities are public.

### Named exports
```js
export function log(message) {
  console.log(message)
}
export const DEFAULT_LEVEL = 'info'
export const LEVELS = {
  error: 0,
  debug: 1,
  warn: 2,
  data: 3,
  info: 4,
  verbose: 5,
}
export class Logger {
  constructor(name) {
    this.name = name
  }
  log(message) {
    console.log(`[${this.name}] ${message}`)
  }
}
```

### Default exports
```js
export default class Logger {
  constructor(name) {
    this.name = name
  }
  log(message) {
    console.log(`[${this.name}] ${message}`)
  }
}
```

### Importing default exports
```js
import MyLogger from './logger.js'
const logger = new MyLogger('info')
logger.log('Hello World')
```

- Default export internally uses the name `default`.
- Using `import * as loggerModule` allows access to `loggerModule.default`.
- `import { default } from './logger.js'` is invalid.
