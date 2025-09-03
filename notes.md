# JavaScript Variables, Scope, and Async/Await

## Variables in JavaScript
Variables are containers for storing data values. In JavaScript, variables can be declared using:
- **var**: Function-scoped, can be redeclared and updated.
- **let**: Block-scoped, can be updated but not redeclared within the same scope.
- **const**: Block-scoped, cannot be updated or redeclared (constant).

### Example
```javascript
var name = "Alice";   // function scoped
let age = 25;         // block scoped
const country = "US"; // constant value
```

---

## Global Variables
A **global variable** is declared outside of any function or block and can be accessed anywhere in the program.

```javascript
var globalVar = "I am global";

function printGlobal() {
  console.log(globalVar); // Accessible here
}
printGlobal();
```

---

## Scope in JavaScript
**Scope** determines the accessibility of variables.

- **Global Scope**: Variables declared outside functions are accessible everywhere.
- **Function Scope**: Variables declared with `var` inside a function are accessible only within that function.
- **Block Scope**: Variables declared with `let` or `const` inside `{}` are accessible only within that block.

```javascript
function testScope() {
  var functionVar = "Only inside function";
  if (true) {
    let blockVar = "Only inside block";
    console.log(blockVar);
  }
  // console.log(blockVar); // Error: blockVar not defined
}
```

---

## Synchronous vs Asynchronous in JavaScript

### Synchronous
Code is executed line by line, waiting for each statement to finish before moving to the next.

```javascript
console.log("Task 1");
console.log("Task 2");
console.log("Task 3");
// Output: Task 1 → Task 2 → Task 3
```

### Asynchronous
Code execution does not block the program. Long-running tasks (like API calls, file operations, or timers) are handled in the background.

```javascript
console.log("Task 1");
setTimeout(() => {
  console.log("Task 2 (delayed)");
}, 2000);
console.log("Task 3");
// Output: Task 1 → Task 3 → Task 2 (after delay)
```

---

## Async/Await

### What is Async/Await?
`async` and `await` provide a simpler way to work with asynchronous code using promises.

- **async**: Declares a function that returns a promise.
- **await**: Pauses execution inside an async function until the promise is resolved.

### Example
```javascript
function fetchData() {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Data received"), 2000);
  });
}

async function getData() {
  console.log("Fetching...");
  const data = await fetchData();
  console.log(data);
}

getData();
// Output: Fetching... → (after 2s) Data received
```

---

## Summary
- Variables can be declared with `var`, `let`, or `const`.
- Global variables are accessible everywhere.
- Scope can be global, function, or block level.
- JavaScript can run synchronously (line by line) or asynchronously (non-blocking).
- `async/await` simplifies working with promises and asynchronous operations.
