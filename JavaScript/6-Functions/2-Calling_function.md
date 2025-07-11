## 1. How do you call a function in JavaScript?

You call a function by using its name followed by parentheses `()`. If the function expects parameters, you pass them inside the parentheses.

#### Example:

```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
}

greet("Alice");  // Calls the function and prints: Hello, Alice!
```
## 2. What happens if you call a function without parentheses?

If you refer to a function **without parentheses**, you get a reference to the function itself, **not the result of executing it**. This means the function does **not run**.

#### Example:

```javascript
function greet() {
  console.log("Hello!");
}

console.log(greet);    // Prints the function definition (function reference)
greet;                 // Reference to the function, but does not call it
```
## 3. What is the result of calling a function with fewer arguments than parameters?

When you call a function with fewer arguments than parameters:

- The missing parameters are assigned the value `undefined`.
- If the function uses those parameters without checking, it may lead to unexpected results or `NaN` (for arithmetic operations).

#### Example:

```javascript
function add(a, b) {
  return a + b;
}

console.log(add(5));   // Output: NaN, because b is undefined
```
To avoid this, you can provide default parameter values:

```javascript
function add(a, b = 0) {
  return a + b;
}

console.log(add(5));   // Output: 5
```
## 4. What is the result of calling a function with more arguments than parameters?

If you call a function with **more arguments** than the number of parameters defined:

- The extra arguments are **ignored** by default.
- However, you can access all passed arguments using the special `arguments` object or rest parameters (`...args`).

#### Example:

```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
}

greet("Alice", "extra", 123);  // Output: Hello, Alice!
// The extra arguments "extra" and 123 are ignored in this function
```
## 5.Can a function return another function? Provide an example.

Yes, a function can **return another function**. This is a common pattern in JavaScript and is used in closures and higher-order functions.

#### Example:

```javascript
function greetMaker(greeting) {
  return function(name) {
    console.log(`${greeting}, ${name}!`);
  };
}

const sayHello = greetMaker("Hello");
sayHello("Alice");  // Output: Hello, Alice!
```
## 6. How can you call a function with a dynamic number of arguments?

You can use:

- The `arguments` object inside the function (available in regular functions).
- Rest parameters syntax (`...args`) to gather all arguments into an array.

#### Using `arguments` object:

```javascript
function sum() {
  let total = 0;
  for (let i = 0; i < arguments.length; i++) {
    total += arguments[i];
  }
  return total;
}

console.log(sum(1, 2, 3, 4));  // Output: 10
```
#### Using rest parameters:
```javascript
function sum(...args) {
  return args.reduce((acc, val) => acc + val, 0);
}

console.log(sum(1, 2, 3, 4));  // Output: 10
```