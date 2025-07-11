## 1. What is the difference between function parameters and function arguments in JavaScript?

- **Parameters** are the named variables listed in a function's definition. They act as placeholders for the values the function expects.

- **Arguments** are the actual values passed to the function when it is called.

Example:

```javascript
function greet(name) {   // `name` is a parameter
  console.log("Hello, " + name);
}

greet("Alice");          // `"Alice"` is an argument
```
## 2. Can you define a function with more parameters than the number of arguments passed? What happens?

- Yes, you can define a function with more parameters than the number of arguments passed during the function call.

- When fewer arguments are provided than parameters, the **extra parameters are assigned the value `undefined`**.

#### Example:

```javascript
function add(a, b, c) {
  console.log(a, b, c);
}

add(1, 2); // Output: 1 2 undefined
```
In this example, `c` is not passed an argument, so it defaults to `undefined`.
## 3. What value is assigned to a parameter when an argument is not passed?

- When a function is called without providing an argument for a parameter, that parameter is assigned the value `undefined` by default.

- To avoid `undefined`, you can specify **default parameter values** in the function definition.

#### Example without default value:

```javascript
function greet(name) {
  console.log("Hello, " + name);
}

greet(); // Output: Hello, undefined
```
#### Example with default value:
```javascript
function greet(name = "Guest") {
  console.log("Hello, " + name);
}

greet(); // Output: Hello, Guest
```
## 4. How does JavaScript treat extra arguments passed to a function with fewer parameters?

- In JavaScript, if you pass **more arguments** than the number of parameters defined in the function, the **extra arguments are not assigned to any named parameters**, but they are **still accessible** within the function.

- These extra arguments do **not cause an error** and are simply ignored unless explicitly accessed.

#### Example:

```javascript
function greet(name) {
  console.log("Hello, " + name);
}

greet("Alice", "Bob", "Charlie"); // Output: Hello, Alice
```
Only the first argument is used (`"Alice"`), the rest are ignored unless accessed manually.
## 5. Can you access all passed arguments inside a function, regardless of parameter count? How?

- **Yes**, you can access all arguments passed to a function even if they don't have corresponding named parameters.

There are two main ways to do this:

#### 1. Using the `arguments` object (non-arrow functions only):

- The `arguments` object is array-like and contains all the arguments passed to the function.

```javascript
function showArguments() {
  for (let i = 0; i < arguments.length; i++) {
    console.log(arguments[i]);
  }
}

showArguments("a", "b", "c"); // Output: a b c
```
Note: `arguments` is not available in arrow functions.
#### 2. Using rest parameters (...args) — ES6+:
- Rest parameters collect all remaining arguments into a real array.

```javascript
function showArguments(...args) {
  args.forEach(arg => console.log(arg));
}

showArguments("a", "b", "c"); // Output: a b c
```
Rest parameters are the modern and preferred approach for accessing all arguments, and they work in both regular and arrow functions.