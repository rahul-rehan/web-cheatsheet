## 1. What is the difference between an arrow function with an expression vs. a block statement body?

- **Expression Body:**
  - Returns the result of the expression **implicitly** (no `return` keyword needed).
  - No curly braces `{}` are used.
  
  ```javascript
  const add = (a, b) => a + b; // Implicit return
  ```
- **Block Body:**

    - Uses curly braces {} to contain multiple statements.

    - Requires an explicit return statement to return a value.

    ```javascript
    const add = (a, b) => {
    const result = a + b;
    return result; // Explicit return required
    };
    ```
## 2. How do you return a value from an arrow function that uses a block body?

- You must use the **`return`** keyword explicitly inside the block body.

#### Example:

```javascript
const multiply = (x, y) => {
  const product = x * y;
  return product; // Explicit return required
};
```
- If you omit the `return` statement, the function will return `undefined`.
## 3. Why is a return statement needed when using braces `{}` in an arrow function body?

- When an arrow function uses **braces `{}`** to define its body (a block body), it behaves like a regular function block.
- In this case, **JavaScript does not return a value implicitly**, so you must use an explicit `return` statement to return a value.
- Without the `return`, the function returns `undefined` by default.

## 4. What is implicit return in arrow functions? Provide an example.

- **Implicit return** occurs when an arrow function has a **concise body** (no braces), and the expression's result is automatically returned without needing the `return` keyword.
  
#### Example:

```javascript
const square = x => x * x; // Implicit return of x * x
console.log(square(4)); // Output: 16
```
- Here, the expression `x * x` is returned automatically.