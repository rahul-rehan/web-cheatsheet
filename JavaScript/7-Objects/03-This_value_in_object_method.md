## 1. What does `this` refer to in an object method?

- Inside an object method, `this` refers to the **object on which the method was called**.
- It allows methods to access and manipulate the object's own properties.

## 2. What is the value of `this` inside a regular object method?

- The value of `this` is the **calling object** (the object before the dot when the method is invoked).
- Example: In `obj.method()`, `this` inside `method` refers to `obj`.

## 3. What happens to the `this` value if a method is assigned to a different object?

- When a method is assigned to another object and called from there, `this` changes to refer to the **new calling object**.
- `this` is determined by how a function is **called**, not where it was defined.

#### Example:

```javascript
const obj1 = {
  name: "Object 1",
  greet() {
    console.log(this.name);
  }
};

const obj2 = {
  name: "Object 2"
};

obj1.greet(); // Output: Object 1

// Assign method to obj2
obj2.greet = obj1.greet;

obj2.greet(); // Output: Object 2
```
## 4. How does the value of `this` change when a method is called using `call()`, `apply()`, or `bind()`?

- `call()` and `apply()` **invoke** a function immediately, allowing you to explicitly set the value of `this` to a specified object.
- `bind()` **returns a new function** with `this` permanently set to the provided object.
- These methods allow overriding the default `this` binding.

#### Example:

```javascript
function greet() {
  console.log(this.name);
}

const person = { name: "Alice" };

greet.call(person);   // Output: Alice
greet.apply(person);  // Output: Alice

const boundGreet = greet.bind(person);
boundGreet();         // Output: Alice
```
## 5. What is the behavior of `this` inside an arrow function defined in an object?

- Arrow functions **do not have their own `this`**.
- Instead, they inherit `this` from their **lexical (surrounding) scope** where they are defined.
- When used inside an object, `this` inside an arrow function usually does **not** refer to the object itself.
- Often, it refers to the **global object** (in non-strict mode) or `undefined` (in strict mode), depending on the context.

#### Example:

```javascript
const obj = {
  name: "Alice",
  arrowFunc: () => {
    console.log(this.name);
  }
};

obj.arrowFunc(); // Output: undefined (or global name if set)
```
## 6. How can incorrect usage of `this` lead to bugs in object methods?

- If `this` loses its intended binding, methods may:
  - Access or modify the wrong object's properties.
  - Return `undefined` or unexpected values.
  - Cause runtime errors or silent failures.
- Common pitfalls include:
  - Extracting a method and calling it standalone, which causes `this` to default to the global object or `undefined`.
  - Using arrow functions as methods when `this` binding to the object is required.
  - Forgetting to bind the correct context when passing methods as callbacks.

#### Example:

```javascript
const obj = {
  name: "Alice",
  greet() {
    console.log(this.name);
  }
};

const greetFunc = obj.greet;
greetFunc(); // Output: undefined, because `this` is lost
```
## 7. Why is `this` undefined in strict mode inside a regular function (not a method)?

- In **non-strict mode**, `this` inside a regular function refers to the **global object** (`window` in browsers).
- In **strict mode**, JavaScript sets `this` to `undefined` in regular functions (not called as methods).
- This behavior prevents unintended access to the global object.

#### Example:

```javascript
"use strict";

function showThis() {
  console.log(this);
}

showThis(); // Output: undefined
```
## 8. How can you ensure the correct `this` context in asynchronous object methods?

- Asynchronous callbacks (e.g., setTimeout, Promise, event listeners) can lose the original this binding.

- To ensure the correct context:

    - Use arrow functions, which inherit this from their lexical scope.

    - Use .bind(this) to explicitly bind the method.

    - Store a reference to this in a variable like self or that (older pattern).

#### Example using arrow function:
```javascript
const obj = {
  name: "Alice",
  delayedGreet() {
    setTimeout(() => {
      console.log(this.name); // Correctly refers to obj
    }, 1000);
  }
};
```
#### Example using .bind(this):
```javascript
const obj = {
  name: "Alice",
  delayedGreet() {
    setTimeout(function() {
      console.log(this.name);
    }.bind(this), 1000);
  }
};
```
## 9. Compare the value of `this` in object methods, arrow functions, and global functions

| Context            | `this` refers to                        |
|--------------------|-----------------------------------------|
| Object method      | The object the method is called on      |
| Arrow function     | The lexical (enclosing) scope's `this` |
| Global function    | Global object (in non-strict mode) or `undefined` (in strict mode) |

#### Example:

```javascript
const obj = {
  name: "Alice",

  regularMethod() {
    console.log("regular:", this.name); // "Alice"
  },

  arrowMethod: () => {
    console.log("arrow:", this.name); // Likely undefined
  }
};

obj.regularMethod(); // Output: "regular: Alice"
obj.arrowMethod();   // Output: "arrow: undefined"
```
Properly understanding how `this` behaves in different contexts helps avoid bugs and unexpected behavior.
#### Global function example:
```javascript
"use strict";

function globalFunc() {
  console.log("global:", this); // undefined in strict mode
}

globalFunc();
```
The behavior of `this` depends on how the function is defined and invoked. Arrow functions do not bind their own `this`, while regular functions and methods do — based on the call context.