## 1. What is variable scope in JavaScript?

- **Variable scope** refers to the region or context in a program where a variable is accessible.
- It determines **where a variable can be read or modified** within the code.
- JavaScript uses scope to control **visibility and lifetime** of variables.

## 2. What are the types of scopes in JavaScript?

1. **Global Scope:**
   - Variables declared outside any function or block.
   - Accessible from anywhere in the code.

2. **Function Scope (Local Scope):**
   - Variables declared inside a function using `var`, `let`, or `const`.
   - Accessible only within that function.

3. **Block Scope:**
   - Variables declared inside a block (e.g., `{ ... }`), using `let` or `const`.
   - Accessible only within that block and nested blocks.

## 3. What is the difference between global scope and local scope?

| Aspect             | Global Scope                               | Local Scope                            |
|--------------------|-------------------------------------------|--------------------------------------|
| **Definition**     | Variables declared outside any function or block | Variables declared inside a function or block |
| **Accessibility**  | Accessible from anywhere in the program   | Accessible only within the specific function or block |
| **Lifetime**       | Exists for the duration of the program    | Exists only during function/block execution |
| **Example**        | `var x = 10;` declared globally           | `function foo() { let y = 5; }`       |

- Global scope variables can be accessed and modified from any part of the code, while local scope variables are limited to their own function or block context.

## 4. What is function scope? Provide an example.

- **Function scope** means that variables declared inside a function are only accessible within that function.
- Variables declared with `var`, `let`, or `const` inside a function cannot be accessed from outside the function.

**Example:**

```js
function greet() {
  var message = "Hello!";
  console.log(message); // Logs "Hello!"
}

greet();
console.log(message); // ReferenceError: message is not defined
```
- Here, `message` is function-scoped and cannot be accessed outside `greet()`.

## 5. What is block scope? Which keywords (var, let, const) support it?

- **Block scope** means variables are accessible only within the block `{ ... }` where they are declared.
- Variables declared with **`let`** and **`const`** are block-scoped.
- Variables declared with **`var`** are **not block-scoped**; they are function-scoped or globally scoped.

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
- `let` and `const` variables `a` and `b` exist only inside the block.

- `var` variable `c` is not block-scoped and is accessible outside the block.