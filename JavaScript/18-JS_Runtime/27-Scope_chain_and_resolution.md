## 1. What is the scope chain in JavaScript?

- The **scope chain** is a hierarchy of scopes that JavaScript uses to resolve variable access.
- It starts from the current execution context's lexical environment and moves outward to parent scopes, up to the global scope.
- Each function or block creates a new scope, and these nested scopes form the chain.

## 2. How does JavaScript resolve variable names using the scope chain?

- When a variable is referenced, JavaScript looks for it in the **current scope** first.
- If not found, it moves **upward through the outer scopes** in the scope chain one by one.
- This continues until the variable is found or the global scope is reached.
- If the variable is not found in any scope, a **ReferenceError** is thrown.

**Example:**

```js
let a = 1; // Global scope

function outer() {
  let b = 2; // Outer function scope

  function inner() {
    let c = 3; // Inner function scope
    console.log(a, b, c); // Accesses variables through scope chain
  }

  inner();
}

outer(); // Logs: 1 2 3
```

## 3. What happens if a variable is not found in any scope?

- If JavaScript cannot find a variable in the current scope or any outer scopes up to the global scope, it throws a **ReferenceError**.
- This means the variable is **undefined** in that context and not declared anywhere accessible.

## 4. How does the call stack relate to the scope chain?

- The **call stack** manages the execution contexts of functions as they are called and returned.
- Each execution context has its own **lexical environment** which forms part of the **scope chain**.
- When a function is invoked, a new execution context with its scope is pushed onto the call stack.
- The scope chain is used during variable resolution within the currently active execution context on top of the call stack.
- Thus, the call stack controls which scope chain is active based on the current function being executed.

## Best Practices and Errors
## 1. How can understanding scope help prevent bugs in your code?

- Knowing how scope works helps you avoid **accidental variable overwrites** and **unexpected variable access**.
- It ensures variables are declared in the correct place and lifetime, preventing bugs related to **variable shadowing** or **leaking globals**.
- Proper scope management improves **code readability**, **maintenance**, and **predictability**.

## 2. What are common mistakes developers make related to variable scope?

- Using `var` unintentionally causing variables to be function-scoped instead of block-scoped.
- Accidentally creating **global variables** by omitting `var`, `let`, or `const`.
- Variable **shadowing** leading to confusion about which variable is accessed.
- Accessing variables **before declaration** leading to bugs with temporal dead zone (TDZ).
- Mixing scopes causing unintended side effects or difficult-to-track bugs.

## 3. How can using let and const help manage scope more safely?

- `let` and `const` are **block-scoped**, limiting variable visibility to the block they are declared in, reducing accidental overwrites.
- They prevent variables from leaking outside their intended scope, minimizing bugs.
- `const` ensures variables cannot be reassigned, adding immutability and safer code practices.
- Together, they reduce common pitfalls associated with `var`.

## 4. What tools or settings (like "use strict", ESLint) help manage scope effectively?

- `"use strict"` enables strict mode which catches common mistakes such as implicit global variables.
- **ESLint** can be configured with rules to warn about undeclared variables, unused variables, or shadowing.
- Modern IDEs and code editors often highlight scope-related issues.
- These tools enforce best practices and help catch scope-related bugs early in development.
