## 1. What is an IIFE (Immediately Invoked Function Expression)?

An **IIFE** (Immediately Invoked Function Expression) is a JavaScript function that runs **immediately after it is defined**. It is a design pattern used to create a new scope and avoid polluting the global namespace.


## 2. What is the Syntax of an IIFE in JavaScript?

An IIFE is typically written as a function expression wrapped inside parentheses, followed by another set of parentheses to invoke it immediately.

**Syntax:**

```js
(function() {
  // code here runs immediately
})();
```
Or using arrow functions:

```js
(() => {
  // code here runs immediately
})();
```
## 3. Why and When Would You Use an IIFE?

- **Avoid global namespace pollution:** Variables inside the IIFE are scoped locally and don’t affect the global scope.
- **Data privacy:** Variables and functions inside an IIFE are not accessible from outside, helping encapsulate logic.
- **Initialization:** Useful for running setup code once without leaving behind temporary variables.
- **Module pattern foundation:** Often used as a base for module patterns before ES6 modules were introduced.

**Example:**

```js
(function() {
  const message = "Hello from IIFE!";
  console.log(message);
})();

// message is not accessible here
// console.log(message); // Error: message is not defined
```
## 4. How Does an IIFE Help with Variable Scoping or Avoiding Global Namespace Pollution?

An IIFE creates a **new function scope** that isolates variables and functions declared inside it from the global scope. This prevents variables from **polluting the global namespace**, avoiding naming collisions and unintended interactions between different parts of code.

Example:

```js
(function() {
  var localVar = "I am local";
  console.log(localVar); // Works fine
})();

console.log(typeof localVar); // undefined — localVar is not in global scope
```
## 5. Can You Define an IIFE Using an Arrow Function? Provide an Example.

Yes, you can define an IIFE using an arrow function by wrapping it in parentheses and immediately invoking it:

```js
(() => {
  console.log("Hello from arrow function IIFE!");
})();
```
## 6. Can IIFEs Return Values? Show How.

Yes, IIFEs can return values that can be assigned to variables:

```js
const result = (function() {
  return 42;
})();

console.log(result); // Output: 42
```
Similarly, with an arrow function:

```js
const result = (() => 42)();

console.log(result); // Output: 42
```
## 7. How Does the Presence or Absence of a Semicolon Before an IIFE Affect Execution?

If an IIFE immediately follows another statement without a terminating semicolon, it can cause a **syntax error** or unexpected behavior because JavaScript might interpret it as a function call on the previous statement’s value.

**Example of problematic code without semicolon:**

```js
const a = 5
(function() {
  console.log("IIFE running");
})();
```
This may be parsed as `5(function(){...})`, which is invalid.

**Solution:** Always place a semicolon before an IIFE if it follows another statement.

```js
const a = 5;
(function() {
  console.log("IIFE running");
})();
```
Or start the IIFE with a semicolon:

```js
;(() => {
  console.log("IIFE running");
})();
```