# Node.js and TypeScript

TypeScript adds static types to JavaScript. It helps catch errors before code runs.

TypeScript cannot run directly in Node.js. It must be compiled to plain JavaScript.

That extra step helps catch bugs early and improves code quality.

## Using TypeScript with Node.js

Install TypeScript:
```
npm install --save-dev typescript
```

Compile a file:
```
npx tsc example.ts
node example.js
```

Tools like `ts-node` and `tsx` let you run TypeScript directly during development.

Install them:
```
npm install --save-dev ts-node
npm install --save-dev tsx
```

Run a file:
```
npx ts-node example.ts
npx tsx example.ts
```

You can also use `tsx` as a loader:
```
node --import=tsx example.ts
```

Loaders let you customize how Node.js loads modules.

## @types/node

Use `@types/node` for TypeScript support in Node.js.

It provides type definitions for Node.js globals and modules.

Install it:
```
npm install --save-dev @types/node
```

This package improves autocompletion and type checking.

## TypeScript in Node.js Today

Node.js is working to make TypeScript easier to run.

As of Node.js 24, you can execute TypeScript files directly with built-in type stripping.

But this supports only erasable TypeScript syntax and ignores `tsconfig.json`.

For full TypeScript support, a runner like `tsx` is still the best choice.

Learn more: nodejsdp.link/node-ts

TypeScript is useful, but not the main focus of this book. The patterns in this book work well in both JavaScript and TypeScript.
