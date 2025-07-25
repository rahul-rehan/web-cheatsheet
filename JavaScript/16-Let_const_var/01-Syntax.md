## 1. What are the key differences between `let`, `var`, and `const`?

| Feature           | `var`                            | `let`                             | `const`                            |
|-------------------|---------------------------------|----------------------------------|----------------------------------|
| Scope             | Function-scoped                  | Block-scoped                     | Block-scoped                     |
| Hoisting          | Hoisted and initialized with `undefined` | Hoisted but not initialized (temporal dead zone) | Hoisted but not initialized (temporal dead zone) |
| Redeclaration     | Allowed                         | Not allowed                      | Not allowed                      |
| Reassignment      | Allowed                         | Allowed                         | Not allowed (constant binding)  |
| Use case          | Legacy, avoid in modern code    | Variables that change value     | Variables with constant value    |

## 2. How do you declare a variable using `let`? Provide an example.

```js
let count = 10;
count = 20;  // Reassignment is allowed
console.log(count); // 20
```
## 3. How do you declare a variable using `const`? What are the restrictions?

- Declared using the `const` keyword.
- Must be initialized at the time of declaration.
- Cannot be reassigned after initialization.
- For objects and arrays, the **binding** is constant, but the content **can be mutated**.

Example:

```js
const PI = 3.14159;
// PI = 3.14; // Error: Assignment to constant variable.

const arr = [1, 2, 3];
arr.push(4); // Allowed - mutation is allowed
console.log(arr); // [1, 2, 3, 4]
```
## 4. Can you reassign a `let` variable? What about a `const` variable?

- **`let` variables** can be reassigned:
  ```js
  let count = 1;
  count = 2; // Allowed
  ```
- `const` variables cannot be reassigned after initialization:

    ```js
    const name = "Alice";
    // name = "Bob"; // Error: Assignment to constant variable.
    ```
## 5. What happens if you try to redeclare a `let` or `const` variable in the same scope?

- Redeclaring a `let` or `const` variable in the **same scope** results in a **SyntaxError**.
- Example:
  ```js
  let value = 10;
  // let value = 20; // SyntaxError: Identifier 'value' has already been declared

  const MAX = 100;
  // const MAX = 200; // SyntaxError: Identifier 'MAX' has already been declared
  ```
- This prevents accidental redeclaration and helps maintain clearer, less error-prone code.