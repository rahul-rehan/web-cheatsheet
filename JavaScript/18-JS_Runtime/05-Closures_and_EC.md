## 1. How do closures relate to execution context and lexical environment?

- A **closure** is created when a function **retains access to its lexical environment** even after its outer function has finished executing.
- This happens because the inner function **remembers the variables and scope** that existed when it was created, not just when it is called.
- The **execution context** of the outer function is popped off the call stack when it finishes, but its **lexical environment is preserved** in memory as long as the inner function (closure) still references it.
- Closures allow functions to access variables from their original lexical environment even when executed outside of that environment.

## 2. What is a closure’s execution context, and when is it preserved?

- A closure's **execution context** is the environment created when the inner function runs.
- However, the key feature of closures is that the **outer function’s lexical environment is preserved**, allowing the inner function to access those variables.
- The outer function’s execution context itself does **not persist** after the function returns, but its **lexical environment** (variable bindings) **is preserved** as long as the closure exists.
- This preservation occurs when the inner function is returned or passed outside the outer function, maintaining access to the outer function’s variables.

---

**Summary:**

| Concept           | Explanation                                              |
|-------------------|----------------------------------------------------------|
| Closure           | Inner function plus preserved lexical environment of outer function. |
| Execution Context  | Active environment when function runs (temporary).       |
| Lexical Environment | Variable environment tied to where function was declared (can be preserved). |
| Preservation      | Outer lexical environment preserved if inner function (closure) still references it after outer function returns. |

## 3. Can multiple closures share the same outer execution context?

- **Yes**, multiple closures can share the **same outer lexical environment** (outer execution context’s variables).
- When an outer function creates multiple inner functions (closures), each inner function maintains a reference to the **same lexical environment** created by the outer function.
- This means all those closures can access and modify the same outer variables, allowing shared state between them.

## 4. How do inner functions access variables from outer execution contexts?

- Inner functions access variables from outer execution contexts via the **scope chain**.
- When a variable is referenced inside an inner function, JavaScript looks first in the inner function’s own lexical environment.
- If the variable is not found, it continues looking up the scope chain to the outer lexical environment(s) until it finds the variable or reaches the global scope.
- This chain of lexical environments enables inner functions to access variables declared in their outer functions, even after those outer functions have returned (closure).

---

**Summary:**

| Question                                   | Answer                                                                                  |
|--------------------------------------------|-----------------------------------------------------------------------------------------|
| Can multiple closures share same outer context? | Yes, multiple closures can share and access the same outer lexical environment variables. |
| How do inner functions access outer variables?    | Via the scope chain that links the inner function’s lexical environment to outer ones.    |
