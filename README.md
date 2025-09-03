# JavaScript Interview Questions & Answers

This document contains **60 JavaScript interview questions** divided into **Basic, Intermediate, and Advanced** levels, with answers and examples.

---

## 🔹 Basic JavaScript Questions (20)

### 1) What are variables in JavaScript?
Variables store data values. Declared using `var`, `let`, or `const`.

```js
let name = "Alice";
const pi = 3.14;
var age = 25;
```

---

### 2) Difference between `var`, `let`, and `const`?
- `var`: function-scoped, hoisted, re-declarable.
- `let`: block-scoped, reassignable.
- `const`: block-scoped, cannot be reassigned.

---

### 3) What is a global variable?
Declared outside all functions, accessible everywhere.

```js
var globalVar = "hello";
```

---

### 4) What are primitive types?
`string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`.

---

### 5) What is `typeof` operator?
Used to check the type.

```js
typeof "abc"; // "string"
typeof 123;   // "number"
```

---

### 6) Difference between `==` and `===`?
- `==`: loose equality (type coercion).
- `===`: strict equality (no coercion).

---

### 7) What is the difference between `null` and `undefined`?
- `undefined`: variable declared but not assigned.
- `null`: intentional empty value.

---

### 8) What are loops in JavaScript?
- `for`
- `while`
- `do...while`
- `for...in`
- `for...of`

---

### 9) Example of `for` loop?
```js
for (let i = 0; i < 3; i++) console.log(i);
```

---

### 10) Example of `while` loop?
```js
let i = 0;
while (i < 3) {
  console.log(i);
  i++;
}
```

---

### 11) Example of `do...while` loop?
```js
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 3);
```

---

### 12) What are functions?
Reusable blocks of code.

```js
function add(a,b){ return a+b; }
```

---

### 13) Difference between function declaration and expression?
- Declaration: `function foo(){}`
- Expression: `const foo = function(){}`

---

### 14) What is an arrow function?
Concise syntax, lexical `this`.

```js
const add = (a,b) => a+b;
```

---

### 15) What is a parameter vs argument?
- Parameter: variable in function definition.
- Argument: actual value passed.

---

### 16) What are template literals?
Strings with backticks and interpolation.

```js
let name="Bob";
console.log(`Hello ${name}`);
```

---

### 17) What is string concatenation?
Joining strings with `+`.

```js
"Hello" + " World";
```

---

### 18) What is an array?
Ordered list of values.

```js
let arr=[1,2,3];
```

---

### 19) What is an object?
Collection of key-value pairs.

```js
let user={name:"Sam",age:20};
```

---

### 20) What are conditional statements?
`if`, `else`, `else if`, `switch`.

```js
if(x>10) console.log("Big");
```

---

## 🔹 Intermediate JavaScript Questions (20)

### 1) Explain scope in JS?
- Global, function, block, module.

---

### 2) What is hoisting?
Declarations moved to top. `var` → `undefined`; `let/const` → TDZ.

---

### 3) Explain closure?
Function that remembers its outer scope.

```js
function counter(){
  let c=0;
  return ()=>++c;
}
```

---

### 4) What is lexical scope?
Scope determined by code structure, not runtime.

---

### 5) What are higher-order functions?
Functions taking/returning functions.

---

### 6) What is `this` keyword?
Dynamic depending on call context.

---

### 7) Example of `call`, `apply`, `bind`?
```js
function greet(msg){ console.log(msg+" "+this.name); }
greet.call({name:"Bob"},"Hi");
```

---

### 8) What is event bubbling?
Events propagate from child → parent.

---

### 9) What is event delegation?
Attaching one event listener to parent to handle child events.

---

### 10) What is the difference between `for...in` and `for...of`?
- `for...in`: iterates keys of object.
- `for...of`: iterates values of iterable.

---

### 11) What is destructuring?
Unpacking arrays/objects.

```js
const {name} = {name:"Tom"};
```

---

### 12) Spread vs Rest operator?
- Spread `...arr` → expands.
- Rest `...args` → collects.

---

### 13) What are default parameters?
```js
function greet(name="Guest"){ console.log(name); }
```

---

### 14) Difference between array methods `map`, `filter`, `reduce`?
- `map`: transform.
- `filter`: select.
- `reduce`: accumulate.

---

### 15) Difference between shallow and deep copy?
- Shallow: copies top-level only.
- Deep: copies nested too.

---

### 16) What is a promise?
Represents future value (pending/fulfilled/rejected).

---

### 17) What are async functions?
Functions declared with `async`, return promise.

---

### 18) Example of async/await?
```js
async function fetchData(){
  let res = await fetch("/api");
}
```

---

### 19) Difference between synchronous and asynchronous?
Sync = blocking; Async = non-blocking.

---

### 20) What is the event loop?
Handles execution of sync & async tasks with call stack, queues.

---

## 🔹 Advanced JavaScript Questions (20)

### 1) What are microtasks vs macrotasks?
- Microtasks: `Promise.then`
- Macrotasks: `setTimeout`, events

---

### 2) What are generators?
Functions that yield values.

```js
function* gen(){ yield 1; yield 2; }
```

---

### 3) What are async generators?
Generators combined with `await`.

---

### 4) What is `WeakMap` and `WeakSet`?
Collections with weak object references.

---

### 5) Difference between `Object.freeze` and `Object.seal`?
- Freeze: no changes.
- Seal: no new properties.

---

### 6) What is currying?
Transforming function of many args into series of functions.

```js
const curry = a=>b=>a+b;
```

---

### 7) What is memoization?
Caching results of expensive function calls.

---

### 8) What are modules in JS?
Reusable code units using `import/export`.

---

### 9) Difference between CommonJS and ES Modules?
- CommonJS → `require`
- ESM → `import/export`

---

### 10) What is tree shaking?
Removing unused code during bundling.

---

### 11) What is the `new` keyword?
Creates instance of constructor function/class.

---

### 12) What is prototype inheritance?
Objects inherit from `prototype` chain.

---

### 13) Difference between `Object.create` and class?
`Object.create` links prototypes; `class` defines constructors.

---

### 14) What is polyfill?
Code that implements modern features in old environments.

---

### 15) What are service workers?
Background scripts for caching/offline in browsers.

---

### 16) What is debouncing?
Delays function execution until after activity stops.

---

### 17) What is throttling?
Ensures function executes at most once per interval.

---

### 18) What is garbage collection?
Automatic memory cleanup of unreachable objects.

---

### 19) What is dynamic vs static typing?
JS is dynamically typed (type checked at runtime).

---

### 20) Explain `call stack` vs `heap`?
- Stack: stores function calls.
- Heap: memory allocation for objects.

---

# ✅ Summary
- **20 Basic** → Variables, loops, basics.  
- **20 Intermediate** → Scope, closure, async basics.  
- **20 Advanced** → Generators, modules, memory, async patterns.

---
