## 1. Are variables declared with `var` hoisted? How does this affect their behavior?

- Yes, variables declared with `var` are **hoisted** to the top of their enclosing function or global scope.
- During hoisting, the **declaration** is moved to the top but **not the initialization**.
- This means you can reference a `var` variable before its declaration without a ReferenceError, but its value will be `undefined` until the assignment line is executed.
- Example:
  ```js
  console.log(x); // undefined (not ReferenceError)
  var x = 5;
  ```
## 2. Are `let` and `const` hoisted? How is their hoisting different from `var`?

- Yes, `let` and `const` declarations are hoisted to the top of their **block scope**.
- Unlike `var`, they are **not initialized** during hoisting.
- Accessing them before their declaration causes a **ReferenceError** due to the **Temporal Dead Zone (TDZ)**.
- This means you cannot use `let` or `const` variables before they are declared in the code.
- Example:
  ```js
  console.log(a); // ReferenceError: Cannot access 'a' before initialization
  let a = 5;
  ```
## 3. What is the temporal dead zone (TDZ) in the context of `let` and `const`?

- The **Temporal Dead Zone (TDZ)** is the time period between entering a scope and the actual declaration of a `let` or `const` variable.
- During the TDZ, the variable exists but **cannot be accessed**.
- Attempting to access the variable before its declaration results in a **ReferenceError**.
- TDZ helps catch errors early by preventing the use of variables before they are properly declared.

## 4. Example of accessing `let` or `const` before declaration causing an error:

```js
{
  // TDZ starts here

  console.log(x); // ReferenceError: Cannot access 'x' before initialization
  let x = 10;

  // TDZ ends after the declaration of x
}
```
```js
{
  // TDZ starts here

  console.log(y); // ReferenceError: Cannot access 'y' before initialization
  const y = 20;

  // TDZ ends after the declaration of y
}
```