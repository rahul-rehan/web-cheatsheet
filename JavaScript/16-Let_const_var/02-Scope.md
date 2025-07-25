## 1. What is the scope of a `var` declared variable?

- Variables declared with `var` have **function scope**.
- They are accessible throughout the entire function in which they are declared.
- If declared outside any function, they have **global scope**.
- `var` declarations are **hoisted** to the top of their scope, initialized with `undefined`.

## 2. What is the scope of `let` and `const` declared variables?

- Variables declared with `let` and `const` have **block scope**.
- They are only accessible within the block (`{ ... }`) where they are defined, such as inside loops, conditionals, or functions.
- They are **not hoisted** in the same way as `var`; accessing them before declaration results in a **ReferenceError** (temporal dead zone).
## 3. How do `let`, `var`, and `const` behave inside a block (`{}`)?

- **`var`**:
  - Has **function scope**, not block scope.
  - If declared inside a block but outside any function, it becomes **globally scoped**.
  - It ignores block boundaries like `{}`.
  
- **`let` and `const`**:
  - Have **block scope**.
  - They exist only within the block `{}` they are declared in.
  - Cannot be accessed outside the block.

## 4. How do `let`, `var`, and `const` behave inside a loop (e.g., `for` loop)?

- **`var`**:
  - Declared variables are **function scoped**.
  - The same variable is reused in each iteration.
  - This can cause issues with closures capturing loop variables.
  
- **`let` and `const`**:
  - Variables are **block scoped** and recreated **fresh in each iteration**.
  - This allows correct capturing of the variable’s value per iteration in closures.
  - `const` must be initialized in each iteration and cannot be reassigned within that iteration.
