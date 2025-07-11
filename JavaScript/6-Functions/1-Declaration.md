## 1. What are the different ways to declare a function in JavaScript?

There are mainly three common ways to declare functions in JavaScript:

1. **Function Declaration**
2. **Function Expression**
3. **Arrow Function Expression**

## 2. What is the syntax of a function declaration?

```javascript
function functionName(parameters) {
  // function body
}
```
### Example:

```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
}
```
## 3. How does a function expression differ from a function declaration?

- **Function Declaration**:  
  - Has a name.  
  - Is hoisted, meaning it can be called before it is defined in the code.

- **Function Expression**:  
  - Can be named or anonymous (usually anonymous).  
  - Is **not** hoisted, so it cannot be called before it is assigned.  
  - Often assigned to a variable.

#### Example of function expression:

```javascript
const greet = function(name) {
  console.log(`Hello, ${name}!`);
};
```
Here, `greet` holds the function, and you cannot call `greet()` before this line executes.
## 4. What is an anonymous function? Provide an example.

An **anonymous function** is a function that **does not have a name**. These functions are often used as arguments to other functions or assigned to variables.

#### Example:

```javascript
const greet = function(name) {
  console.log(`Hello, ${name}!`);
};
greet("Alice");  // Output: Hello, Alice!
```
Here, the function assigned to `greet` is anonymous because it has no name.
## 5. What is an arrow function? How is it different from a regular function?

An **arrow function** is a concise syntax for writing functions introduced in ES6. It uses the `=>` (arrow) notation.

#### Example:

```javascript
const add = (a, b) => a + b;
console.log(add(2, 3));  // Output: 5
```
**Differences from regular functions:**

- **Syntax:** Arrow functions have a shorter syntax.

- **`this` binding:** Arrow functions do **not** have their own `this`; they inherit `this` from the surrounding scope.

- **No `arguments` object:** Arrow functions do **not** have their own `arguments` object.

- **Cannot be used as constructors:** Arrow functions cannot be used with the `new` keyword.
```javascript
// Regular function has its own 'this'
function regular() {
  console.log(this);
}

// Arrow function inherits 'this'
const arrow = () => {
  console.log(this);
};
```
## 6. Can functions be stored in variables or passed as arguments?

Yes, in JavaScript, **functions are first-class citizens**, which means:

- Functions can be **stored in variables**.
- Functions can be **passed as arguments** to other functions.
- Functions can also be **returned from other functions**.

#### Example:

```javascript
const greet = function(name) {
  console.log(`Hello, ${name}!`);
};

function callFunction(fn, value) {
  fn(value);
}

callFunction(greet, "Alice");  // Output: Hello, Alice!
```
## 7. Can you define a function inside another function in JavaScript?

Yes, you can **define a function inside another function**. This is called a **nested function** or **inner function**.

- The inner function is only accessible within the outer function.
- It can access variables from the outer function's scope (closure).

#### Example:

```javascript
function outer() {
  function inner() {
    console.log("Hello from inner function!");
  }
  inner();
}

outer();  // Output: Hello from inner function!
```