# Using Modules in TypeScript

- TypeScript is a superset of JavaScript.
- It integrates with browsers, Node.js, and other environments.
- TypeScript handles modules both in input syntax and output emission.
- It can compile ES module code to CommonJS and vice versa.

## The compiler's role
- Detect module syntax in source files.
- Resolve imports based on host environment.
- Emit compatible JavaScript module format.
- Assign accurate types to imported entities.

## Example
```ts
import sayHello from 'greetings'
sayHello('world')
```

TypeScript must know:
- whether `greetings` resolves to `greetings.ts` or `greetings.js`.
- whether the target runtime expects ESM or CommonJS.
- whether the imported file is TypeScript or compiled JavaScript.
- whether the imported module is ESM or CommonJS.

## Key compiler options
- `module`: controls emitted module format.
- `moduleResolution`: controls how imports are resolved.
- `verbatimModuleSyntax`: keeps import/export syntax stable.

## Recommended Node.js settings
```json
{
  "compilerOptions": {
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "verbatimModuleSyntax": true
  }
}
```

## Input vs output
- Input syntax may be ES modules.
- Output may be ESM or CommonJS.
- Compiler options determine the emitted module kind.
- A file that looks like ESM may still compile to CommonJS.

## Module resolution in TypeScript
- TypeScript follows Node-style resolution when configured for Node.js.
- It supports path aliases and custom mappings.
- The compiler needs to know whether a package is ESM or CommonJS.

## Practical advice
- Prefer `NodeNext` for modern Node.js projects.
- Keep module settings explicit and consistent.
- Understand the host environment for correct import resolution.

## Summary
- TypeScript can bridge module systems.
- Configuration is critical for correct behavior.
- Clear settings make imports and exports predictable.
