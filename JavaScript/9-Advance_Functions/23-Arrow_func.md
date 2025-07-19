## 1. What is an arrow function in JavaScript?

- An **arrow function** is a concise syntax for writing function expressions introduced in ES6.
- It provides a shorter way to write functions and lexically binds the `this` value, unlike regular functions.

## 2. What is the basic syntax of an arrow function?

- Basic syntax:

```javascript
// With parentheses and braces
const func = (param1, param2) => {
  // function body
  return param1 + param2;
};

// With implicit return (no braces)
const func = (param1, param2) => param1 + param2;

// Single parameter without parentheses
const square = x => x * x;

// No parameters
const greet = () => console.log("Hello!");
```
## 3. How do arrow functions improve code readability or brevity?

- **Concise syntax:** Eliminates the need for the `function` keyword and sometimes braces/`return` keyword.
- **Implicit return:** Single-expression functions can return values without an explicit `return`.
- **Lexical `this`:** Arrow functions inherit `this` from their surrounding scope, reducing the need for `.bind()` or workarounds like `var self = this`.
- **Improved readability:** Especially useful for short callbacks or functional programming patterns.
## 4. Are arrow functions anonymous by default?

- Yes, **arrow functions are anonymous by default**, meaning they do not have a name unless assigned to a variable or used as an object property.
- When assigned to a variable, the function gets the variable name for identification in stack traces and debugging.

#### Example:

```javascript
const add = (a, b) => a + b;

console.log(add.name); // Output: "add"
```
- If used inline without assignment, the arrow function remains unnamed:

```javascript
setTimeout(() => console.log("Hello!"), 1000);
```
- Although anonymous, arrow functions can still be identified by their variable or property assignment.