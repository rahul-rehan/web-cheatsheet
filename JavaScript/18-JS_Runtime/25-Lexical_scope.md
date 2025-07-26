## 1. What is lexical (or static) scope in JavaScript?

- Lexical scope means that the scope of a variable is determined by its **physical location** in the source code.
- The structure of the code (how functions and blocks are nested) defines the scope hierarchy **at compile time**, not at runtime.

## 2. How is lexical scope determined?

- Lexical scope is determined **when the code is written**, based on where functions and variables are declared.
- Inner functions have access to variables declared in their outer (enclosing) functions or global scope.

## 3. Can an inner function access variables from its outer function? Why?

- Yes, an inner function **can access** variables from its outer function because of lexical scoping.
- The inner function carries a reference to its outer function’s scope, allowing it to access those variables even after the outer function has finished execution (this also forms the basis of **closures**).

**Example:**

```js
function outer() {
  let outerVar = 'I am outside!';

  function inner() {
    console.log(outerVar); // Can access outerVar due to lexical scope
  }

  inner();
}

outer(); // Outputs: I am outside!
```
## 4. How does lexical scope enable closures?

- Lexical scope allows inner functions to remember and access variables from their outer function's scope even after the outer function has finished executing.
- This **preserved access** to the outer scope is what creates a **closure**.
- Closures enable functions to maintain private state and create powerful patterns like data encapsulation and function factories.

## 5. Provide a code example demonstrating lexical scope.

```js
function outer() {
  let count = 0; // Variable in outer scope

  function inner() {
    count++; // Accesses and modifies outer scope variable
    console.log(count);
  }

  return inner; // Returns the inner function, forming a closure
}

const counter = outer();
counter(); // Outputs: 1
counter(); // Outputs: 2
counter(); // Outputs: 3
```