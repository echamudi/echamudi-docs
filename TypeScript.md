# TypeScript

## Import index.d.ts from js file.

```js
/// <reference path="../jmdict-util/types/index.d.ts"/>
```

## Type of instance of a class
```ts
let a: InstanceType<typeof SomeClass>
```