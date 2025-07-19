## 1. What is lexical scoping in JavaScript?

- **Lexical scoping** means that a function’s scope is determined by its **physical placement in the source code**.
- In JavaScript, variables are resolved by looking at the **location where the function was defined**, not where it was called.

## 2. How does lexical scoping relate to closures?

- Closures are a direct result of lexical scoping.
- Because JavaScript functions remember the **scope in which they were defined**, they can **retain access to variables** from their outer (lexical) environment even after that environment has exited.
- This preserved access is what creates a **closure**.

#### Example:

```javascript
function outer() {
  const outerVar = 'I am from outer scope';

  function inner() {
    console.log(outerVar); // inner still has access due to lexical scoping
  }

  return inner;
}

const myClosure = outer();
myClosure(); // Output: I am from outer scope
```
## 3. How does JavaScript determine variable resolution using lexical scoping?

JavaScript resolves variables using a **scope chain** that is established at the time a function is defined, not when it is executed.

#### Resolution Steps:

1. **Local Scope**: JavaScript first checks the variable in the current (local) function scope.
2. **Outer Lexical Environments**: If not found, it looks in the outer functions' scopes, moving outward through the lexical scope chain.
3. **Global Scope**: If the variable is not found in any enclosing functions, it checks the global scope.
4. **ReferenceError**: If the variable is still not found, JavaScript throws a `ReferenceError`.

#### Example:

```javascript
let globalVar = 'global';

function outer() {
  let outerVar = 'outer';

  function inner() {
    let innerVar = 'inner';
    console.log(globalVar); // 'global'
    console.log(outerVar);  // 'outer'
    console.log(innerVar);  // 'inner'
  }

  inner();
}

outer();
```
#### In this example:

- `innerVar` is resolved in the local scope of `inner()`.

- `outerVar` is resolved from the enclosing lexical scope (`outer()`).

- `globalVar` is resolved from the global scope.

This behavior is a core part of lexical scoping, where variable resolution is based on the code structure, not the call stack.
## 4. Example That Demonstrates Lexical Scope

Lexical scope means that the scope of a variable is determined by its position in the source code. Inner functions have access to variables declared in their outer (parent) functions.

#### Example:

```javascript
function outer() {
  const outerVariable = 'I am from the outer scope';

  function inner() {
    console.log(outerVariable); // Can access outerVariable due to lexical scoping
  }

  inner();
}

outer();
```
#### Explanation:
- The `inner()` function is defined inside `outer()`, so it has access to `outerVariable` even though that variable is not declared within `inner()`.

- This access is possible because of lexical scoping, where the JavaScript engine resolves variable references based on where functions are defined, not where they are called.
## 5. What’s the difference between lexical scoping and dynamic scoping?

| Feature               | Lexical Scoping (JavaScript)                          | Dynamic Scoping                          |
|-----------------------|--------------------------------------------------------|-------------------------------------------|
| Scope is determined by | **Where the function is written** in the source code  | **Where the function is called** at runtime |
| Variable lookup       | Uses the **static structure** of nested scopes         | Uses the **call stack** to find variables |
| Example languages     | JavaScript, Python, C++                                | Bash, some older Lisps                    |

#### JavaScript uses **lexical scoping**:
```javascript
let name = 'Global';

function outer() {
  let name = 'Outer';

  function inner() {
    console.log(name); // Lexical scope: 'Outer'
  }

  inner();
}

outer();
```
## 6. How does lexical scope affect variable shadowing?

- **Variable shadowing** happens when a variable declared in a local (inner) scope has the same name as a variable in an outer scope.
- Due to **lexical scoping**, the variable in the innermost scope **shadows** or **overrides** access to the variable with the same name in the outer scope.
- This means that inside the inner scope, references to the variable name will resolve to the closest declaration.

#### Example:

```javascript
const message = 'Global message';

function printMessage() {
  const message = 'Local message'; // This shadows the global variable
  console.log(message);            // Output: 'Local message'
}

printMessage();
console.log(message);              // Output: 'Global message'
```
- In the example, inside `printMessage()`, the local `message` variable shadows the global one.

- Outside the function, the global `message` remains unchanged and accessible.