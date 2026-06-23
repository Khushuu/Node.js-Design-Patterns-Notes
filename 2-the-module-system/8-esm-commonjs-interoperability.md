# ES Modules and CommonJS Interoperability

- ES modules and CommonJS are different module systems.
- Interoperability is possible but requires care.

## Strict mode
- ES modules run in strict mode implicitly.
- CommonJS requires `'use strict'` manually.
- Strict mode disallows undeclared variables and `with`.

## Top-level await
- ES modules support top-level `await`.
- CommonJS requires `await` inside an async function.

```js
// main.mjs
import { loadData } from 'someModule'
console.log(await loadData())
```

```js
// main.cjs
'use strict'
const { loadData } = require('someModule')
async function main() {
  console.log(await loadData())
}
main()
```

## `this` behavior
- ES modules: top-level `this` is `undefined`.
- CommonJS: top-level `this === exports`.

## Missing CommonJS references in ES modules
- `require`, `exports`, `module.exports`, `__filename`, `__dirname` are not defined.
- Use `import.meta` for module metadata.

```js
const __filename = import.meta.filename
const __dirname = import.meta.dirname
```

## Importing CommonJS from ES modules
- Default import works for CommonJS modules.
- Named exports may fail if the CommonJS module does not expose them.

```js
import someModule from './someModule.cjs'
const { someFeature } = someModule
console.log(someFeature)
```

- Alternative: recreate `require()` with `createRequire()`.

```js
import { createRequire } from 'node:module'
const require = createRequire(import.meta.url)
const { someFeature } = require('./someModule.cjs')
console.log(someFeature)
```

## Importing ES modules from CommonJS
- `require('./someModule.mjs')` may fail with `ERR_REQUIRE_ESM`.
- Use dynamic `import()` instead.

```js
'use strict'
async function main() {
  const { someFeature } = await import('./someModule.mjs')
  console.log(someFeature)
}
main()
```

- Dynamic import is asynchronous.
- CommonJS cannot use top-level `await`.

## Importing JSON files
- CommonJS can import JSON directly with `require('./sample.json')`.
- ES modules require a type annotation.

```js
import data from './sample.json' with { type: 'json' }
```

- Dynamic JSON import uses `with: { type: 'json' }`.

```js
const { default: data } = await import('./sample.json', {
  with: { type: 'json' },
})
```

- Alternative: read and parse JSON manually.

```js
import { readFile } from 'node:fs/promises'
import { join } from 'node:path'
const jsonPath = join(import.meta.dirname, 'sample.json')
const dataRaw = await readFile(jsonPath, 'utf-8')
const data = JSON.parse(dataRaw)
console.log(data)
```

- Or use `createRequire()` in ES modules.

## Key points
- ES modules can import CommonJS via default import.
- CommonJS can import ES modules with dynamic `import()`.
- JSON import syntax in ESM is explicit for security.
