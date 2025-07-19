## 1. What is an IIFE in JavaScript?

- An **Immediately Invoked Function Expression (IIFE)** is a function that is defined and executed immediately after its creation.
- It creates a new scope, helping to avoid polluting the global namespace.
- IIFEs are commonly used to **encapsulate code** and **create private scopes**.

## 2. What is the syntax of a basic IIFE?

```javascript
(function() {
  // Code inside IIFE
  console.log("This runs immediately!");
})();
```
- The function is wrapped in parentheses `()` to turn it into an expression.

- The trailing `()` immediately invokes the function.

- Alternatively, you can use arrow functions:

```javascript
(() => {
  console.log("This also runs immediately!");
})();
```
## 3. Why are IIFEs used in JavaScript?

- To **immediately execute a function** right after it is defined.
- To **create a new scope** that encapsulates variables and functions, preventing them from polluting the global scope.
- To **avoid naming conflicts** by limiting variable visibility.
- To **organize code** and maintain privacy for variables.

## 4. What problem does an IIFE solve in older JavaScript code?

- Before ES6 introduced block-scoped variables (`let` and `const`), JavaScript only had function scope with `var`.
- This made it hard to create private variables or avoid variable conflicts in the global scope.
- IIFEs provide a way to **simulate block scope** by creating a private function scope for variables.
- This prevents variables from leaking into or clashing with the global scope or other code.

## 5. How does an IIFE help create a private scope?

- An IIFE defines a function and **immediately invokes it**, creating a **new lexical scope**.
- Variables and functions declared inside the IIFE are **local to that function scope**.
- These variables are **not accessible outside** the IIFE, effectively making them private.
- This encapsulation prevents external code from accessing or modifying those variables.

#### Example:

```javascript
(function() {
  var privateVar = "I'm private";
  console.log(privateVar); // Accessible here
})();

console.log(typeof privateVar); // undefined — not accessible outside
```
## 6. Can an IIFE accept arguments? Provide an example.

- Yes, an IIFE can accept arguments just like any other function.
- You pass arguments by including them inside the invoking parentheses.

#### Example:

```javascript
(function(name) {
  console.log(`Hello, ${name}!`);
})('Alice'); // Output: Hello, Alice!
```
## 7. Can an IIFE return a value?

- Yes, an IIFE can return a value.
- The returned value can be stored in a variable or used immediately.

#### Example:

```javascript
const result = (function(a, b) {
  return a + b;
})(5, 3);

console.log(result); // Output: 8
```
## 8. How does the function declaration inside an IIFE differ from a regular function declaration?

- Function declarations inside an IIFE are **local to the IIFE’s scope**.
- These functions are **not accessible outside** the IIFE, unlike regular function declarations which are hoisted to their containing scope.
- This scoping helps **prevent naming collisions** and keeps helper functions **private** within the IIFE.

#### Example:

```javascript
(function() {
  function helper() {
    console.log("I'm inside the IIFE");
  }
  helper(); // Works here
})();

helper(); // ReferenceError: helper is not defined
```
## 9. Is an IIFE executed once or multiple times?

- An IIFE is **executed immediately once** at the moment it is defined.
- It is not called again unless explicitly invoked elsewhere (which is uncommon).
- Its primary purpose is to create a new scope and run code immediately.

## 10. Can arrow functions be used to write an IIFE? Provide an example.

- Yes, arrow functions can be used to create IIFEs.
- The syntax is similar, but you wrap the arrow function in parentheses and invoke it immediately.

#### Example:

```javascript
(() => {
  console.log("This is an IIFE using an arrow function!");
})();
```