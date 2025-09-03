
# JavaScript — The Best-Practice Crash Course (with Code & Q&A)

> A fast, practical path to learning modern JavaScript. Each section includes a short explanation, a runnable code sample, and key takeaways. At the end, you’ll find an **“Important JavaScript Questions & Answers”** section to test yourself.

---

## 0) How to Use This File
- Read one section per day, **type** every code sample yourself.
- After each section, try the **Practice** prompt.
- Revisit the **Q&A** section weekly.

---

## 1) Setup & Hello World

**What & Why:** Use your browser console or Node.js to run JS.

```html
<!-- index.html -->
<!doctype html>
<html>
  <body>
    <h1>Hello JS</h1>
    <script>
      console.log("Hello, world!");
      document.body.insertAdjacentHTML("beforeend", "<p>JS is running ✅</p>");
    </script>
  </body>
</html>
```

**Practice:** Create a page that logs your name and shows the current time.

---

## 2) Variables: `let`, `const`, `var`

**What & Why:** Prefer `const` by default; use `let` when reassignment is needed; avoid `var` (function-scoped, hoisted).

```js
const pi = 3.14159;
// pi = 4  // ❌ TypeError (don’t reassign const)

let count = 0;
count += 1; // ✅

function demoVar() {
  if (true) {
    var x = 42; // function-scoped
    let y = 99; // block-scoped
  }
  console.log(typeof x, typeof y); // "number", "undefined"
}
demoVar();
```

**Key:** Block scope prevents leaks; choose `const` unless you must reassign.

---

## 3) Types & Type Coercion

**What & Why:** JS has 8 built-in types. Beware coercion.

- Primitive: `string`, `number`, `bigint`, `boolean`, `undefined`, `symbol`, `null`
- Structural: `object` (including arrays, functions)

```js
console.log(typeof null); // "object" (legacy quirk)
console.log(+"2" + 1);    // 3 (unary + coerces)
console.log("5" - 2);     // 3
console.log(0 == false);  // true  (loose)
console.log(0 === false); // false (strict)
```

**Key:** Prefer `===` and `!==`. Know when coercion helps/hurts.

---

## 4) Strings & Template Literals

```js
const name = "Ada";
const message = `Hello, ${name.toUpperCase()}! Today is ${new Date().toDateString()}.`;
console.log(message);
```

**Practice:** Build a sentence from an array of words using `join(" ")`.

---

## 5) Numbers & Math

```js
console.log((0.1 + 0.2).toFixed(2)); // "0.30" (floating-point)
const rand = Math.floor(Math.random() * 6) + 1; // dice 1-6
```

**Key:** Floating-point is imprecise; avoid equality on decimals.

---

## 6) Arrays — Essentials

```js
const nums = [1, 2, 3];
nums.push(4);
const doubled = nums.map(n => n * 2);   // [2,4,6,8]
const evens = nums.filter(n => n % 2 === 0); // [2,4]
const sum = nums.reduce((a, b) => a + b, 0); // 10
```

**Practice:** From `[1,2,3,4,5]` get squares of odds only.

---

## 7) Objects & Destructuring

```js
const user = { id: 1, name: "Ada", role: "admin" };
const { name, ...rest } = user;
console.log(name, rest); // "Ada" {id:1, role:"admin"}

const withDefaults = ({limit = 10, offset = 0} = {}) => ({limit, offset});
console.log(withDefaults({limit:5})); // {limit:5, offset:0}
```

---

## 8) Functions: Declarations vs Expressions, Arrow Functions

```js
function add(a, b) { return a + b; } // hoisted

const multiply = function(a, b) { return a * b; }; // not hoisted

const square = x => x * x; // concise arrow
```

**Key:** Arrows don’t have their own `this`, `arguments`, `super`, or `new.target`.

---

## 9) Scope, Hoisting & Closures

```js
function makeCounter() {
  let count = 0;          // captured by closure
  return () => ++count;   // inner function remembers outer scope
}
const next = makeCounter();
console.log(next(), next()); // 1 2
```

**Key:** A closure is formed when a function retains access to its lexical scope.

---

## 10) `this`, `call`, `apply`, `bind`

```js
const obj = {
  x: 7,
  show() { console.log(this.x); }
};

const show = obj.show;
show();           // undefined in strict mode (or window.x in sloppy)
show.call(obj);   // 7
const bound = show.bind(obj);
bound();          // 7 (forever bound)
```

---

## 11) Prototypes, Classes & Inheritance

```js
class Person {
  constructor(name) { this.name = name; }
  greet() { return `Hi, I'm ${this.name}`; }
}
class Dev extends Person {
  constructor(name, stack) { super(name); this.stack = stack; }
  greet() { return `${super.greet()} and I use ${this.stack}`; }
}
console.log(new Dev("Ada", "JS").greet());
```

**Key:** Classes are syntax sugar over prototypal inheritance.

---

## 12) Modules (ESM)

```js
// math.js
export const add = (a,b) => a + b;
export default function sub(a,b){ return a - b; }

// app.js
import sub, { add } from "./math.js";
console.log(add(2,3), sub(5,2));
```

**Key:** Use ESM (`import/export`) in modern tooling/browsers or Node with `"type":"module"`.

---

## 13) The Event Loop, Tasks & Microtasks

```js
console.log("A");
setTimeout(() => console.log("B (macrotask)"), 0);
Promise.resolve().then(() => console.log("C (microtask)"));
console.log("D");
// Output order: A, D, C, B
```

**Key:** Microtasks (promises) run before the next macrotask.

---

## 14) Promises & `async/await`

```js
const wait = ms => new Promise(res => setTimeout(res, ms));

async function demo() {
  console.log("Start");
  await wait(300);
  console.log("After 300ms");
}
demo();
```

**Practice:** Fetch two URLs in parallel with `Promise.all`.

---

## 15) Fetching Data

```js
async function getUser(id) {
  const res = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`);
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return await res.json();
}
getUser(1).then(u => console.log(u.name)).catch(console.error);
```

**Key:** Always handle `.ok`/errors; consider timeouts/abort.

---

## 16) Error Handling & `try/catch/finally`

```js
async function safe(fn) {
  try {
    return await fn();
  } catch (err) {
    console.error("Problem:", err.message);
    return null;
  } finally {
    console.log("Cleanup runs regardless");
  }
}
```

---

## 17) DOM Basics

```html
<div id="app"></div>
<script>
  const app = document.getElementById("app");
  const btn = document.createElement("button");
  btn.textContent = "Click me";
  btn.addEventListener("click", () => {
    app.insertAdjacentHTML("beforeend", "<p>Clicked!</p>");
  });
  app.appendChild(btn);
</script>
```

---

## 18) Events, Delegation & Bubbling

```html
<ul id="list">
  <li data-id="1">One</li>
  <li data-id="2">Two</li>
</ul>
<script>
  document.getElementById("list").addEventListener("click", e => {
    if (e.target.matches("li")) {
      console.log("Clicked item", e.target.dataset.id);
    }
  });
</script>
```

**Key:** Delegate events to a parent for dynamic lists.

---

## 19) Forms & Validation

```html
<form id="f">
  <input name="email" type="email" required />
  <button>Submit</button>
</form>
<script>
  document.getElementById("f").addEventListener("submit", e => {
    e.preventDefault();
    const form = new FormData(e.target);
    console.log(Object.fromEntries(form)); // { email: "..." }
  });
</script>
```

---

## 20) Storage: `localStorage` / `sessionStorage`

```js
localStorage.setItem("theme", "dark");
const theme = localStorage.getItem("theme");
localStorage.removeItem("theme");
```

---

## 21) Maps, Sets, WeakMap, WeakSet

```js
const set = new Set([1,2,2,3]);       // {1,2,3}
const map = new Map([["a",1],["b",2]]);
const wm = new WeakMap();             // keys must be objects
```

**Key:** Use `Map` for non-string keys, `Set` for uniqueness.

---

## 22) Iterables, Iterators & Generators

```js
function* range(start, end) {
  for (let i = start; i <= end; i++) yield i;
}
console.log([...range(3,5)]); // [3,4,5]
```

---

## 23) Debounce & Throttle (Performance)

```js
const debounce = (fn, ms=300) => {
  let t;
  return (...args) => {
    clearTimeout(t);
    t = setTimeout(() => fn(...args), ms);
  };
};

const throttle = (fn, ms=300) => {
  let last = 0;
  return (...args) => {
    const now = Date.now();
    if (now - last >= ms) {
      last = now;
      fn(...args);
    }
  };
};
```

---

## 24) Pattern: Pure vs. Impure Functions

```js
// Pure: output depends only on inputs; no side effects
const add = (a,b) => a + b;

// Impure: relies on external state
let counter = 0;
function inc() { counter++; }
```

---

## 25) Defensive Programming & Immutability

```js
const user = { id: 1, name: "Ada" };
const renamed = { ...user, name: "Lovelace" }; // shallow copy
```

---

## 26) Basic Testing (No Framework)

```js
function expect(actual) {
  return {
    toBe(expected) {
      if (actual !== expected) throw new Error(`Expected ${expected} got ${actual}`);
    }
  };
}
(function test() {
  expect(1+1).toBe(2);
  console.log("All tests passed");
})();
```

---

## 27) Node.js Quick Intro

```bash
npm init -y
node app.js
```

```js
// app.js
import fs from "node:fs/promises";
const text = await fs.readFile("./app.js", "utf8");
console.log(text.slice(0, 30));
```

---

## 28) NPM Scripts & Tooling

```json
{
  "name": "demo",
  "type": "module",
  "scripts": {
    "dev": "node app.js",
    "test": "node test.js"
  }
}
```

---

## 29) Optional: TypeScript (Why it helps)

- Catches type mistakes early, improves tooling & refactors.
- Start with JSDoc types or migrate gradually.

```js
/**
 * @param {number} a
 * @param {number} b
 * @returns {number}
 */
function add(a,b){ return a+b; }
```

---

# Important JavaScript Questions & Answers

> Use these to self-quiz. Answers are short and practical.

### 1) What’s the difference between `let`, `const`, and `var`?
- `const`: block-scoped, no reassignment.
- `let`: block-scoped, reassignment allowed.
- `var`: function-scoped, hoisted; avoid in modern code.

### 2) What is hoisting?
- Declarations are moved to the top of their scope at compile time. Functions are hoisted fully; `let/const` are in a temporal dead zone until declared.

### 3) Explain closures.
- A function that remembers variables from its lexical scope even when executed outside that scope.

```js
function outer() { let x = 1; return () => x++; }
```

### 4) `==` vs `===`?
- `==` performs type coercion. `===` compares type + value. Prefer `===`.

### 5) `null` vs `undefined`?
- `undefined`: variable declared but not assigned.  
- `null`: intentional absence of value.

### 6) How does the event loop schedule tasks?
- Call stack executes; task queues (macrotasks like `setTimeout`) & microtasks (promises). Microtasks run before the next macrotask.

### 7) What is `this` in different contexts?
- Depends on call site:
  - Method call: object before dot.
  - Standalone function: `undefined` in strict mode.
  - Bound with `bind/call/apply`: explicit.
  - Arrow functions: lexical `this`.

### 8) What’s prototypal inheritance?
- Objects inherit from a prototype chain. `class` syntax wraps prototypes.

### 9) What are pure functions and why?
- No side effects, same input → same output. Easier to test; fewer bugs.

### 10) How to avoid callback hell?
- Use promises and `async/await`. Compose with `Promise.all`, `Promise.race`.

### 11) What does `map`, `filter`, `reduce` do?
- Transform, select, combine (respectively).

### 12) How do you clone an object?
- Shallow: `{...obj}` or `Object.assign({}, obj)`.
- Deep: `structuredClone(obj)` (modern), or libraries/custom.

### 13) Why is `(0.1 + 0.2) !== 0.3`?
- IEEE-754 floating-point imprecision.

### 14) How to debounce/throttle?
- See implementations above; debounce delays, throttle limits rate.

### 15) Difference between `for...of` and `for...in`?
- `for...of` iterates values of an iterable.  
- `for...in` iterates enumerable keys (including inherited) of an object.

### 16) What is a generator?
- A function that can pause/resume, producing an iterator (`function*` and `yield`).

### 17) What are Symbols used for?
- Unique property keys, avoiding name collisions; well-known symbols customize behavior.

### 18) How to handle fetch errors?
- Check `res.ok`, throw on failure; use `try/catch`. Consider AbortController.

### 19) When to use `localStorage` vs cookies?
- `localStorage`: client-only, not sent to server.  
- Cookies: sent with requests; use for server/session needs; secure & httpOnly flags recommended.

### 20) What is tree-shaking?
- Removing unused exports at build time (ESM enables better tree-shaking).

### 21) What’s the difference between `undefined` property and missing property?
- `obj.hasOwnProperty("k")` vs `"k" in obj` or `Object.hasOwn(obj, "k")`.
- `obj.k === undefined` doesn’t distinguish missing vs explicitly set to `undefined`.

### 22) What is currying?
- Transforming `f(a,b)` into `f(a)(b)` for partial application.

```js
const add = a => b => a + b;
```

### 23) What does `Object.freeze` do?
- Makes an object immutable at the top level (shallow). No add/remove/update of properties.

### 24) Difference between `splice` and `slice`?
- `slice(start,end)`: non-mutating copy.  
- `splice(start,count,...)`: mutates array.

### 25) How does optional chaining work?
- `obj?.a?.b` short-circuits to `undefined` if any part is `null/undefined`.

### 26) Nullish coalescing `??` vs `||`?
- `??` only falls back on `null` or `undefined`.  
- `||` also falls back on falsy values like `0`, `""`, `false`.

### 27) How to ensure immutability with arrays?
- Use `concat`, `slice`, spread; avoid mutating methods (`push`, `splice`) or copy first.

### 28) Why prefer arrow functions in callbacks?
- Concise and lexical `this`. Avoid for methods needing their own `this`.

### 29) Explain `Promise.all`, `allSettled`, `race`, `any`.
- `all`: all fulfill or one rejects.  
- `allSettled`: wait for all, give statuses.  
- `race`: first settled (fulfilled/rejected).  
- `any`: first fulfilled (ignores rejections until all reject).

### 30) What is event delegation and why?
- Attach one listener on a parent; handle child events via `e.target`. Efficient for dynamic lists.

### 31) What is a polyfill?
- Code that implements a modern API in older environments.

### 32) How to deep-compare two objects?
- Serialize with caution, or recursively compare keys/values; consider libraries.

### 33) What is `use strict`?
- Strict mode removes silent errors, changes `this` defaults, disallows some syntax.

### 34) Explain temporal dead zone (TDZ).
- Region between entering scope and declaration where `let/const` exist but can’t be accessed.

### 35) Difference between `.forEach` and `map`?
- `.forEach` ignores return values (side effects).  
- `map` returns a new array with transformed items.

### 36) What is a tagged template literal?
- A function that processes a template’s parts:

```js
function tag(strings, ...vals) { return strings[0] + vals.map(String).join("|"); }
tag`a ${1} b ${2}`; // "a 1|2"
```

### 37) Explain `Object.defineProperty`.
- Add or modify a property with descriptors (writable, enumerable, configurable, getters/setters).

### 38) What is the difference between shallow and deep copy?
- Shallow copies share nested object references; deep copies don’t.

### 39) How to prevent XSS when inserting HTML?
- Prefer `textContent`; when using `innerHTML`, sanitize input.

### 40) What is a service worker?
- Background script for PWA: caching, offline, push notifications (beyond this course’s scope).

---

## Bonus Practice Projects (small → bigger)
1. **Counter App**: Buttons for +1/−1 with debounce on input.
2. **Todo List**: Add, toggle, delete; store in `localStorage`.
3. **Fetch Dashboard**: Fetch users, show cards, handle errors/loading.
4. **Timer**: Start/stop/pause; show elapsed microtask vs macrotask demo.
5. **Autocomplete**: Debounced fetch against a public API.

---

## Learning Plan (4 Weeks)
- **Week 1**: Sections 1–10 + Project 1
- **Week 2**: Sections 11–18 + Project 2
- **Week 3**: Sections 19–24 + Project 3
- **Week 4**: Sections 25–29 + Projects 4–5 + Q&A drill

---

## Cheat Sheet: Must-Know Snippets

```js
// 1) Safe JSON parse
const safeJSON = s => { try { return JSON.parse(s); } catch { return null; } };

// 2) Unique array
const unique = arr => [...new Set(arr)];

// 3) Group by key
const groupBy = (arr, key) =>
  arr.reduce((acc, x) => ((acc[x[key]] ??= []).push(x), acc), {});

// 4) Retry fetch
async function retry(fn, times=3) {
  let last;
  for (let i=0;i<times;i++) { try { return await fn(); } catch (e) { last = e; } }
  throw last;
}
```

---

**You’ve got this.** Keep practicing, keep shipping.
