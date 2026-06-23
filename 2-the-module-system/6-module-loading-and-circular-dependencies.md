# Module Loading and Circular Dependencies

- ES modules use a dependency graph to load modules in the correct order.
- The interpreter builds the graph from the entry point and follows imports recursively.
- The loading process has three phases.

## Phase 1 — Construction (Parsing)
- Identify all import statements.
- Recursively load module source files.
- Build the full dependency graph.
- No code execution occurs yet.

## Phase 2 — Instantiation
- Create named references for all exports.
- Link imports and exports.
- Values remain uninitialized.
- Still no code execution.

## Phase 3 — Evaluation
- Execute module code in dependency order.
- Assign actual values to exports.
- The entry point runs last.

## Why this matters
- Imports must be static.
- The graph must be complete before execution.
- This design enables live bindings and better circular dependency support.

## Read-only live bindings
- Imported bindings are read-only references.
- The original module can update the value.
- The consumer cannot reassign the imported binding.

```js
// counter.js
export let count = 0
export function increment() {
  count++
}

// main.js
import { count, increment } from './counter.js'
console.log(count) // 0
increment()
console.log(count) // 1
count++ // TypeError: Assignment to constant variable!
```

## Circular dependencies
- Circular dependencies happen when modules import each other.
- ES modules support circular references with live bindings.
- CommonJS handles cycles differently and may expose partially initialized values.

### Example setup
```js
// a.js
import * as bModule from './b.js'
export let loaded = false
export const b = bModule
loaded = true

// b.js
import * as aModule from './a.js'
export let loaded = false
export const a = aModule
loaded = true

// main.js
import * as a from './a.js'
import * as b from './b.js'
console.log('a ->', a)
console.log('b ->', b)
```

## Example result
- `a` and `b` contain references to each other.
- `loaded` appears `true` in both modules.
- Circular structures are maintained as references.

## How ES modules enable this
- Parsing builds the graph once.
- Instantiation links modules before evaluation.
- Evaluation initializes exports bottom-up.
- Live references keep modules synchronized.
