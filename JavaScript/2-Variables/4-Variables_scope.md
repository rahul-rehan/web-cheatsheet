# Variables Scope

## 1. What is variable scope in JavaScript?

**Variable scope** refers to the **context** or **region** in a program where a variable is **accessible** or **visible**. It determines where a variable can be used or referenced in the code.

---

## 2. What is the difference between block scope, function scope, and global scope?

- **Global Scope:**  
  Variables declared outside any function or block have global scope. They are accessible anywhere in the code.

- **Function Scope:**  
  Variables declared with `var` inside a function are scoped to that entire function. They are accessible anywhere within that function, but not outside of it.

- **Block Scope:**  
  Variables declared with `let` or `const` inside a block (e.g., inside `{}` of an if statement, loop, or function) are scoped only to that block and cannot be accessed outside it.

**Example:**
```javascript
if (true) {
  var functionScoped = 'I am function scoped';
  let blockScoped = 'I am block scoped';
  const alsoBlockScoped = 'Me too';
}

console.log(functionScoped); // Outputs: 'I am function scoped'
console.log(blockScoped);    // ReferenceError: blockScoped is not defined
console.log(alsoBlockScoped);// ReferenceError: alsoBlockScoped is not defined
```

## 3. Which keywords (`var`, `let`, `const`) are block-scoped in JavaScript?

- **`let`** and **`const`** are **block-scoped**. They are limited to the block `{ ... }` where they are defined.
- **`var`** is **function-scoped** and **not block-scoped**. It ignores block boundaries and is scoped to the nearest function.

---

**Summary:**

| Keyword | Scope Type     |
|---------|----------------|
| `var`   | Function scope |
| `let`   | Block scope    |
| `const` | Block scope    |

## 4. Which keyword is function-scoped in JavaScript?

The keyword **`var`** is function-scoped in JavaScript. Variables declared with `var` are accessible throughout the entire function they are declared in, regardless of block boundaries.

---

## 5. What is block scope? Provide a code example.

**Block scope** means that variables declared inside a block (i.e., within `{ ... }`) are only accessible within that block and cannot be accessed outside of it. This applies to variables declared using `let` and `const`.

**Example:**
```javascript
{
  let blockScoped = 'I exist only inside this block';
  const anotherBlockScoped = 42;
  console.log(blockScoped);       // Outputs: I exist only inside this block
  console.log(anotherBlockScoped); // Outputs: 42
}

console.log(blockScoped);        // ReferenceError: blockScoped is not defined
console.log(anotherBlockScoped); // ReferenceError: anotherBlockScoped is not defined
```
## 6. What is function scope? Provide a code example.

**Function scope** means variables declared inside a function using `var` are accessible anywhere within that function, regardless of any inner blocks.

**Example:**
```javascript
function example() {
  if (true) {
    var functionScoped = 'I am accessible anywhere in this function';
  }
  console.log(functionScoped); // Outputs: I am accessible anywhere in this function
}

example();

console.log(functionScoped); // ReferenceError: functionScoped is not defined
```

## 7. What is global scope? How can variables be declared in global scope?

- **Global scope** refers to variables that are accessible **anywhere** in the entire JavaScript program.
- Variables declared **outside of any function or block** automatically have global scope.
- Variables declared with `var` outside a function, or declared without `var`, `let`, or `const` (which is discouraged), become global.
- In browsers, global variables become properties of the `window` object.

**Examples:**
```javascript
var globalVar = 'I am global';
let globalLet = 'Also global';
const globalConst = 'Global constant';

function test() {
  console.log(globalVar);   // Accessible
  console.log(globalLet);   // Accessible
  console.log(globalConst); // Accessible
}

test();

console.log(globalVar);   // Accessible
console.log(globalLet);   // Accessible
console.log(globalConst); // Accessible
```
## 28. How does JavaScript determine the scope of a variable during execution?

- JavaScript uses **lexical scoping** (also called static scoping), which means the scope of variables is determined by their position in the **source code** at the time the code is written, not where functions are called.
- When the code runs, JavaScript creates **scope chains** to resolve variable references by looking up through nested scopes.
- Variables are searched first in the **local scope**, then in the **outer scopes**, and finally in the **global scope** if not found locally.

---

## 9. Can a block-scoped variable be accessed outside the block? Explain.

- **No**, a block-scoped variable declared with `let` or `const` **cannot be accessed outside the block** in which it was declared.
- Attempting to do so results in a **ReferenceError** because the variable’s visibility is limited strictly to the block `{ ... }`.

**Example:**
```javascript
{
  let blockVar = 'Inside block';
}
console.log(blockVar); // ReferenceError: blockVar is not defined
```
This behavior helps prevent accidental access or modification of variables outside their intended scope, improving code safety and clarity.

## 10. Can a function-scoped variable be accessed outside the function? Why or why not?

- **No**, a function-scoped variable declared with `var` **cannot be accessed outside the function** in which it is declared.
- This is because function scope limits the variable’s visibility strictly to the function body.
- Attempting to access it outside the function results in a **ReferenceError** since the variable does not exist in the outer/global scope.

**Example:**
```javascript
function example() {
  var funcScoped = 'I am inside the function';
}
console.log(funcScoped); // ReferenceError: funcScoped is not defined
```

## 11. What happens if you declare a variable without any keyword (`var`, `let`, or `const`)?

- Declaring a variable **without any keyword** creates an **implicit global variable** (in non-strict mode).
- This means the variable becomes a property of the global object (`window` in browsers), which can lead to unintended side effects and bugs.
- It is considered **bad practice** and should be avoided.
- In **strict mode** (`'use strict';`), assigning a variable without declaration throws a **ReferenceError**.

**Example (non-strict mode):**
```javascript
function foo() {
  implicitGlobal = 42; // Creates a global variable implicitly
}
foo();
console.log(implicitGlobal); // Outputs: 42
```

Example (strict mode):
```javascript
'use strict';
function foo() {
  implicitGlobal = 42; // ReferenceError: implicitGlobal is not defined
}
foo();
```

## 12. How does variable shadowing work across different scopes in JavaScript?

- **Variable shadowing** occurs when a variable declared in an inner scope (e.g., inside a function or block) has the **same name** as a variable declared in an outer scope.
- The inner variable **"shadows"** or **overrides** the outer variable within its scope, meaning references to that variable name inside the inner scope access the inner variable, not the outer one.
- Outside the inner scope, the outer variable remains accessible as usual.

**Example:**
```javascript
let name = 'Outer';

function greet() {
  let name = 'Inner';  // Shadows the outer 'name'
  console.log(name);   // Outputs: Inner
}

greet();
console.log(name);     // Outputs: Outer
```
## 13. Can global variables be accessed inside functions and blocks?

- **Yes**, global variables are accessible inside functions and blocks unless they are **shadowed** by a local variable with the same name.
- This means functions and blocks can freely read and modify global variables unless explicitly overridden by local declarations.

**Example:**
```javascript
let globalVar = 'I am global';

function showGlobal() {
  console.log(globalVar); // Outputs: I am global
}

if (true) {
  console.log(globalVar); // Outputs: I am global
}

showGlobal();
```
## 14. How do `let` and `const` behave inside a for loop compared to `var`?

- **`let` and `const` inside a for loop:**
  - Both `let` and `const` are **block-scoped**.
  - In a `for` loop, a **new binding** is created for each iteration, so each loop iteration gets its own independent copy of the variable.
  - This behavior is useful in closures inside loops (e.g., with callbacks or `setTimeout`).

- **`var` inside a for loop:**
  - `var` is **function-scoped**, not block-scoped.
  - There is only **one shared variable** for all iterations.
  - This often causes unexpected behavior, especially in asynchronous code inside loops.

**Example demonstrating the difference:**
```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log('var:', i), 100);
}
// Outputs: var: 3 (three times), because `i` is shared and equals 3 after the loop

for (let j = 0; j < 3; j++) {
  setTimeout(() => console.log('let:', j), 100);
}
// Outputs: let: 0, let: 1, let: 2, each iteration has its own `j`
```

## 15. Give an example showing how improper use of variable scope can lead to bugs.

**Example: Using `var` in a loop causing unexpected behavior**
```javascript
function createFunctions() {
  var funcs = [];

  for (var i = 0; i < 3; i++) {
    funcs.push(function() {
      console.log(i);
    });
  }

  return funcs;
}

const functions = createFunctions();
functions[0](); // Outputs: 3 (unexpected)
functions[1](); // Outputs: 3 (unexpected)
functions[2](); // Outputs: 3 (unexpected)
```

**Explanation:**  
Because `var` is function-scoped, all functions share the same `i` variable, which has the value `3` after the loop ends. This leads to all functions logging `3` instead of `0`, `1`, and `2`.

**Corrected version using `let`:**

```javascript
function createFunctions() {
  let funcs = [];

  for (let i = 0; i < 3; i++) {
    funcs.push(function() {
      console.log(i);
    });
  }

  return funcs;
}

const functions = createFunctions();
functions[0](); // Outputs: 0
functions[1](); // Outputs: 1
functions[2](); // Outputs: 2
```
Using let creates a new binding for each loop iteration, fixing the bug.

## 16. How does scope chaining work in JavaScript?

- **Scope chaining** is the process JavaScript uses to resolve variable references.
- When a variable is accessed, JavaScript first looks in the **current (local) scope**.
- If the variable is not found, it moves up to the **outer (parent) scope**, continuing this process up the chain until it reaches the **global scope**.
- If the variable is not found anywhere in the scope chain, a **ReferenceError** is thrown.

**Example:**
```javascript
let a = 1;

function outer() {
  let b = 2;

  function inner() {
    let c = 3;
    console.log(a, b, c); // Accesses variables through scope chain
  }

  inner();
}

outer(); // Outputs: 1 2 3
```

## 17. What is lexical scoping in JavaScript?

- **Lexical scoping** means the scope of variables is determined by their **physical location in the source code**.
- Inner functions have access to variables declared in their outer (enclosing) functions, regardless of where they are called from.
- The scope is fixed at **compile time**, not at runtime.

---

## 18. How do closures relate to variable scopes in JavaScript?

- A **closure** is created when a function **remembers and has access to variables from its lexical scope even after the outer function has finished execution**.
- Closures allow inner functions to continue accessing the outer function’s variables, enabling powerful patterns like data encapsulation and function factories.

**Example:**
```javascript
function outer() {
  let count = 0;

  return function inner() {
    count++;
    console.log(count);
  };
}

const counter = outer();
counter(); // Outputs: 1
counter(); // Outputs: 2
```
Here, `inner` forms a closure over the variable `count` in `outer`'s scope.

## 19. What is the output of the following code:
```javascript
{ let a = 5; }
console.log(a);
```

**Answer:**  
The output will be a **ReferenceError**, specifically:

```vbnet
ReferenceError: a is not defined
```

**Why?**  
The variable `a` is declared with `let` inside a block `{ ... }`, so it has **block scope**.

This means `a` only exists within that block and is not accessible outside it.

When `console.log(a)` runs outside the block, `a` is not defined, causing the error.

## What is the output of the following code:
```javascript
function test() {
  var b = 10;
}
console.log(b);
```
**Answer:**  
The output will be a **ReferenceError**, specifically:

```vbnet
ReferenceError: b is not defined
```
**Why?**  
The variable `b` is declared with `var` inside the function `test()`, so it has **function scope**.

This means `b` only exists within the `test` function and is not accessible outside it.

Since `console.log(b)` is called outside the function, `b` is not defined in that scope, causing the error.
