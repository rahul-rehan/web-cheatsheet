## 1. What happens when a function and variable have the same name in the same scope? Which gets hoisted?

- When a **function declaration** and a **variable declared with `var`** share the same name in the same scope:
  - Both are hoisted, but **function declarations have higher priority** in hoisting.
  - The function declaration is hoisted first (including its body).
  - The `var` declaration is hoisted afterward, but only the declaration part (not the assignment).
  - If the variable is assigned a value later, it **overwrites** the function reference.

**Example:**

```js
console.log(foo); // Outputs: function foo() {...}

var foo = 5;

function foo() {
  console.log("I am a function");
}

console.log(foo); // Outputs: 5
```
### Explanation:

- Initially, `foo` refers to the **function** due to function hoisting.

- The `var foo` declaration is hoisted, but its **assignment** (`foo = 5`) happens during execution, **overwriting** the function.

- So, **before the assignment**, `foo` is the function; **after the assignment**, `foo` is the number `5`.

## 2. What is the behavior of a `var` variable when accessed before its declaration?

- A `var` variable is **hoisted** to the top of its scope and **initialized with `undefined`**.
- Accessing a `var` variable **before its declaration line** will return `undefined` instead of causing an error.

**Example:**

```js
console.log(a); // Output: undefined
var a = 10;
console.log(a); // Output: 10
```
- This happens because the declaration `var a` is hoisted and initialized as `undefined` during the creation phase, while the assignment `a = 10` occurs later during execution.

## 3. How is the hoisting of arrow functions different from traditional function declarations?

- **Traditional function declarations** are fully hoisted: both their name and body are moved to the top of their scope, allowing them to be called before their definition.
- **Arrow functions**, usually assigned to variables (e.g., `const fn = () => {}`), behave like **function expressions**.
  - Only the variable declaration is hoisted (if declared with `var`), but the assignment (arrow function itself) is **not** hoisted.
  - If declared with `let` or `const`, they are hoisted but remain in the **Temporal Dead Zone (TDZ)** and cannot be accessed before declaration.
- As a result, arrow functions **cannot be invoked before their definition**, unlike traditional function declarations.

## 4. Can you hoist class declarations in JavaScript? Why or why not?

- **Class declarations are hoisted, but not initialized.**
- They behave like variables declared with `let` or `const`: they are in the **Temporal Dead Zone (TDZ)** until the class declaration is evaluated.
- Trying to access or instantiate a class **before its declaration** results in a **ReferenceError**.
- This design prevents the use of classes before they are fully defined.

**Example:**

```js
const c = new MyClass(); // ReferenceError: Cannot access 'MyClass' before initialization

class MyClass {
  constructor() {
    console.log("Hello");
  }
}
```
## 5. How does hoisting behave in strict mode ("use strict") in JavaScript?

- The **hoisting mechanism itself does not change** when using strict mode.
- However, strict mode enforces **stricter runtime rules** which affect variable usage:
  - Variables declared with `let` and `const` still exhibit the Temporal Dead Zone (TDZ) behavior.
  - Using variables before declaration results in immediate **ReferenceErrors**.
  - Assigning to undeclared variables or other unsafe actions throw errors rather than silently failing.
- Strict mode promotes cleaner, safer code but **does not alter how hoisting works fundamentally**.

**Example:**

```js
"use strict";

console.log(a); // undefined (var is hoisted)
var a = 5;

console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 10;
```
