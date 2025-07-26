## 1. How does hoisting work within the execution context?

- **Hoisting** is the process during the **creation phase** of an execution context where variable and function declarations are moved to the top of their scope before code execution.
- Function declarations are hoisted **completely**, meaning both their name and definition are available before the code runs.
- Variable declarations using `var` are hoisted by **allocating memory and initializing with `undefined`**.
- This allows variables and functions to be referenced before their actual declaration lines in the code without causing a reference error (though `undefined` may be returned for `var` variables).

## 2. How are var, let, and const treated differently during the creation phase?

| Declaration Type | Behavior During Creation Phase                                       |
|------------------|---------------------------------------------------------------------|
| **`var`**        | - Declared and initialized with `undefined` (hoisted).<br>- Accessible anywhere within the function or global scope. |
| **`let`**        | - Declared but **not initialized**.<br>- Exists in the **Temporal Dead Zone (TDZ)** until initialized.<br>- Cannot be accessed before declaration (ReferenceError). |
| **`const`**      | - Declared but **not initialized**.<br>- Also exists in the **TDZ**.<br>- Must be initialized at the time of declaration.<br>- Access before initialization throws ReferenceError. |

## 3. What is the temporal dead zone (TDZ), and how is it connected to execution context?

- The **Temporal Dead Zone (TDZ)** is the time period between the start of a scope's execution context **creation phase** and the point where a `let` or `const` variable is initialized.
- During the TDZ, the variables are in scope but **cannot be accessed**; attempting to do so results in a **ReferenceError**.
- The TDZ ensures variables declared with `let` and `const` are not accessible before their actual declaration line in the code, helping prevent bugs related to uninitialized variables.

---

**Summary:**

| Concept          | Explanation                                                 |
|------------------|-------------------------------------------------------------|
| Hoisting         | Moving declarations to the top of the scope during creation phase. |
| `var`            | Hoisted and initialized with `undefined`.                   |
| `let` & `const`  | Hoisted but **not initialized**; blocked by TDZ until declared. |
| Temporal Dead Zone (TDZ) | Period where `let`/`const` exist but are uninitialized and inaccessible. |

## 4. How is scope determined by the execution context?

- The **scope** defines the accessibility of variables and functions at a given point in the code.
- In JavaScript, **scope is determined lexically**, meaning it is based on the **location of the code in the source file**.
- Each execution context has a **scope chain** created during the **creation phase**, which includes its own variables plus references to outer (parent) lexical environments.
- When resolving variable references, JavaScript looks up the scope chain starting from the current execution context to outer contexts until it finds the variable or reaches the global scope.

## 5. What is the difference between lexical scope and dynamic scope in this context?

| Aspect             | Lexical Scope                               | Dynamic Scope                           |
|--------------------|--------------------------------------------|---------------------------------------|
| Definition         | Scope determined by the **physical location** of code in the source. | Scope determined by the **call stack (runtime call chain)**. |
| How variables are resolved | Variable lookups follow the **static nesting** of functions (scope chain). | Variable lookups depend on the **calling function** at runtime. |
| Example in JavaScript | JavaScript uses lexical scope: inner functions have access to variables of outer functions where they were defined. | Dynamic scope is not used in JavaScript but is seen in some other languages. |
| Effect on Execution Context | Execution context holds a reference to its lexical environment for scope resolution. | Execution context would depend on how and where functions are called dynamically. |

---

**Summary:**

- JavaScript uses **lexical scope**, so scope is fixed based on where functions and variables are declared.
- The **execution context** contains the scope chain reflecting lexical scope.
- **Dynamic scope** (not used in JavaScript) would determine scope based on the calling context instead of declaration location.
