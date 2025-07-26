## 1. What is block scope in JavaScript?

- **Block scope** means variables are only accessible within the block `{ ... }` where they are declared.
- A block is typically defined by curly braces, such as in `if`, `for`, `while`, or any `{}`.

## 2. Which declaration keywords support block scope?

- **`let`** and **`const`** support block scope.
- **`var`** does **not** support block scope; it is function-scoped or globally scoped.

## 3. How do let and const behave inside if, for, or while blocks?

- Variables declared with `let` and `const` inside these blocks are confined to the block and cannot be accessed outside it.

**Example:**

```js
if (true) {
  let a = 10;
  const b = 20;
  var c = 30;
  console.log(a, b, c); // 10 20 30
}

console.log(a); // ReferenceError: a is not defined
console.log(b); // ReferenceError: b is not defined
console.log(c); // 30 (var is function/global scoped)
```
- Here, `a` and `b` exist only inside the `if` block, while `c` declared with `var` is accessible outside.

## 4. Does `var` have block scope? Prove with an example.

- No, `var` **does not have block scope**; it is function-scoped or globally scoped.
- Even if declared inside a block, a `var` variable is accessible outside that block within the function or global scope.

**Example:**

```js
if (true) {
  var x = 10;
}
console.log(x); // Outputs: 10
```
- Despite being declared inside the `if` block, `x` is accessible outside because `var` ignores block scope.

## 5. What happens when a `let` variable is accessed before declaration inside its block?

- Accessing a `let` variable before its declaration within the same block causes a **ReferenceError**.
- This occurs because of the **Temporal Dead Zone (TDZ)** — the period from the start of the block until the variable is declared and initialized.

**Example:**

```js
{
  console.log(a); // ReferenceError: Cannot access 'a' before initialization
  let a = 5;
}
```
- In this example, `a` is in the scope but uninitialized until the declaration line, so trying to use it earlier throws an error.