## 1. What is variable shadowing in JavaScript?

- **Variable shadowing** occurs when a variable declared in an inner scope (e.g., inside a function or block) has the same name as a variable in an outer scope.
- The inner variable **"shadows"** or overrides access to the outer variable within its scope.

## 2. Can shadowing lead to bugs? Why or why not?

- Yes, shadowing **can lead to bugs** because it may cause confusion about which variable is being accessed or modified.
- Developers might unintentionally manipulate the inner variable thinking it’s the outer one, leading to unexpected behavior or difficult-to-debug errors.
- Clear naming conventions and careful scoping can help avoid such issues.

## 3. How do block-scoped and function-scoped variables behave when shadowed?

- **Block-scoped variables** (`let`, `const`):
  - When shadowed, the inner variable is limited to its block.
  - The outer variable remains accessible outside that block.
  
- **Function-scoped variables** (`var`):
  - Shadowing occurs within the function scope.
  - The inner variable hides the outer one throughout the entire function.

**Example:**

```js
let x = 10;

function test() {
  let x = 20; // Shadows outer x within this function
  if (true) {
    let x = 30; // Shadows x inside this block only
    console.log(x); // 30
  }
  console.log(x); // 20
}

console.log(x); // 10
test();
```

## 4. Is it a good practice to shadow global variables inside a function? Why or why not?

- Generally, **it is not good practice** to shadow global variables inside functions.
- Shadowing global variables can cause confusion and bugs, as it becomes unclear whether the code refers to the global or local variable.
- It reduces code readability and makes maintenance harder.
- Avoiding shadowing helps prevent unintended side effects and improves clarity.
- Prefer using unique variable names and minimizing dependence on globals for cleaner, safer code.
