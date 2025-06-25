# JavaScript Hoisting Interview Questions and Answers

## 1. What is hoisting in JavaScript?

Hoisting is a JavaScript mechanism where variable and function declarations are moved to the top of their containing scope (either global or function scope) during the compile phase before the code is executed. This means you can use variables and functions before they are declared in the code.

---

## 2.  Which types of declarations are hoisted in JavaScript?

- **Variable declarations using `var`** are hoisted and initialized with `undefined`.
- **Function declarations** are hoisted along with their definitions, allowing them to be called before their declaration.
- **Variables declared with `let` and `const`** are hoisted but **not initialized**, which means they cannot be accessed before their declaration due to the Temporal Dead Zone (TDZ).

---

## 3. How does hoisting differ between `var`, `let`, and `const`?

| Declaration | Hoisted? | Initialization | Temporal Dead Zone (TDZ) | Access Before Declaration Behavior |
|-------------|-----------|----------------|-------------------------|------------------------------------|
| `var`       | Yes       | Initialized to `undefined` | No                      | Returns `undefined`                 |
| `let`       | Yes       | Not initialized | Yes                     | Throws `ReferenceError`             |
| `const`     | Yes       | Not initialized | Yes                     | Throws `ReferenceError`             |

- `var` variables are hoisted and initialized to `undefined`, so they can be accessed before the line where they are declared but will return `undefined`.
- `let` and `const` are hoisted but remain uninitialized until their actual declaration, so accessing them before declaration causes a `ReferenceError` due to the TDZ.

## 4. Are function declarations hoisted? If so, how?

Yes, **function declarations** are fully hoisted in JavaScript. This means both the function's name and its body are moved to the top of their containing scope during the compile phase. As a result, you can call a function declared this way **before** its actual declaration in the code.

```js
// This works because function declarations are hoisted
sayHello();

function sayHello() {
  console.log("Hello!");
}
```

## 5. Are function expressions hoisted? What is the difference from function declarations?

**Function expressions** are **not hoisted** in the same way as function declarations.

- When a function expression is declared using `var`, **only the variable declaration** is hoisted to the top of the scope, not the assignment.
- This means the variable exists during the hoisting phase but is initialized as `undefined`.

So, trying to call the function **before the assignment** results in a runtime error because `undefined` is **not callable**.

#### Example:

```js
sayHello(); // ❌ TypeError: sayHello is not a function

var sayHello = function () {
  console.log("Hello!");
};
```

If `let` or `const` is used to declare the function expression variable, it is **hoisted but uninitialized** (i.e., it resides in the **Temporal Dead Zone** or TDZ).  
Accessing it before the declaration will throw a **ReferenceError**.

---

### 📋 Summary of the Difference

| **Aspect**                        | **Function Declaration**                   | **Function Expression**                                               |
|----------------------------------|--------------------------------------------|------------------------------------------------------------------------|
| **Hoisted?**                     | Yes, both name and body                    | Variable declaration hoisted, but assignment is **not** hoisted       |
| **Can be called before declaration?** | ✅ Yes                              | ❌ No (causes a runtime error)                                         |
| **Scope**                        | Function or global scope                   | Depends on the variable declaration (`var`, `let`, or `const`)        |

---

## 6. What happens if you try to access a `const` variable before it’s declared?

Accessing a `const` variable before its declaration results in a **ReferenceError**.

This is because `const` (like `let`) is hoisted but **not initialized** during the hoisting phase. It resides in the **Temporal Dead Zone (TDZ)** from the start of its scope until the line where it is declared.

```js
console.log(x); // ReferenceError
const x = 10;
```

## 7. What is the Temporal Dead Zone (TDZ), and how is it related to hoisting?

The **Temporal Dead Zone (TDZ)** is the period between the start of a block scope and the point where a variable declared with `let` or `const` is initialized.

- Variables declared with `let` and `const` are hoisted to the top of their block, but are **not initialized**.
- During the TDZ, any attempt to access them results in a **ReferenceError**.
- The TDZ ends once the variable's declaration is encountered in the code.

### Example:

```js
{
  console.log(a); // ReferenceError
  let a = 5;
}
```
Here, `a` is in the TDZ from the start of the block until `let a = 5;` is evaluated.


## 8. Are class declarations hoisted in JavaScript?

Yes, **class declarations are hoisted**, but similar to `let` and `const`, they are **not initialized** during hoisting.

- Attempting to access a class before its declaration will result in a **ReferenceError** due to the **Temporal Dead Zone (TDZ)**.

### Example:

```js
const obj = new MyClass(); // ReferenceError

class MyClass {
  constructor() {
    console.log('Constructor called');
  }
}
```

---
## 9. How Does JavaScript Internally Treat Hoisted Variables During the Creation Phase?
---

During the **creation phase** of the JavaScript execution context, the JavaScript engine **allocates memory for variables and functions** before any code is executed. This is where **hoisting** occurs.

### Here's how different declarations are treated:

* ### `var` Declarations:
    * **Declaration is hoisted** to the top of the scope.
    * **Initialized with `undefined`**.
    * You can access it before its declaration (though the value will be `undefined`).

    ```javascript
    console.log(x); // undefined
    var x = 10;
    ```

* ### `let` and `const` Declarations:
    * **Declaration is hoisted, but not initialized.**
    * They are placed in a **Temporal Dead Zone (TDZ)** from the start of the block until the actual declaration is encountered.
    * Accessing them before initialization results in a `ReferenceError`.

    ```javascript
    console.log(y); // ReferenceError
    let y = 20;
    ```

* ### Function Declarations:
    * Both the **function name and body are hoisted**.
    * You can call the function before its definition in the code.

    ```javascript
    greet(); // "Hello!"
    function greet() {
      console.log("Hello!");
    }
    ```

---
### Summary:
---

* The creation phase sets up the environment.
* `var` is hoisted and initialized with `undefined`.
* `let` and `const` are hoisted but left uninitialized (in TDZ).
* Functions are fully hoisted with their definitions.

This behavior is essential to understand when debugging variable reference issues or unexpected outputs in JavaScript.


## 10. Explain how variable and function hoisting occurs in the global execution context.

In the **global execution context**, JavaScript goes through two phases: the **creation phase** and the **execution phase**. Hoisting primarily occurs during the **creation phase**.

1.  **Creation Phase:**
    * The JavaScript engine scans the entire code.
    * For every `var` declaration it finds, it sets up a property on the global object (e.g., `window` in browsers) with the variable name and initializes its value to `undefined`.
    * For every `function declaration` it finds, it sets up a property on the global object with the function's name and stores the entire function definition (its code block) directly.

2.  **Execution Phase:**
    * The code is executed line by line.
    * When a `var` variable is encountered during execution, it's assigned its actual value, overwriting the `undefined`.
    * When a function declaration is encountered during execution, its definition is already available and can be called.

**In essence, "hoisting" means that declarations of variables (with `var`) and functions are conceptually moved to the top of their scope during the compilation phase.** This allows you to reference them before they appear in the code. However, it's crucial to remember that only the *declaration* is hoisted, not the *initialization* for `var` variables.

---

## 11. Can you explain the difference in hoisting behavior between the following?
`function foo() {}` vs `var foo = function() {}`

This is a key distinction in JavaScript hoisting:

1.  **`function foo() {}` (Function Declaration):**
    * **Hoisting Behavior:** The entire function declaration (both the name `foo` and its code block) is hoisted to the top of its scope.
    * **Availability:** This means you can call `foo()` *before* its actual declaration in the code.
    * **Example:**

        ```javascript
        foo(); // This will work and execute the function
        function foo() {
          console.log("Hello from function declaration!");
        }
        ```

2.  **`var foo = function() {}` (Function Expression):**
    * **Hoisting Behavior:** Only the `var` variable declaration (`var foo`) is hoisted to the top of its scope and initialized with `undefined`. The assignment of the anonymous function to `foo` happens only when that line of code is executed.
    * **Availability:** If you try to call `foo()` *before* the line where it's assigned the function, it will be `undefined` and trying to invoke `undefined` as a function will result in a `TypeError`.
    * **Example:**

        ```javascript
        // foo(); // TypeError: foo is not a function (at this point, foo is undefined)
        var foo = function() {
          console.log("Hello from function expression!");
        };
        foo(); // This will work
        ```

---

## 12. What would be the result of the following code and why?
`foo(); function foo() { console.log("Hello"); }`

**Result:**
Hello

**Why:**

This is a classic example of **function hoisting**.

During the **creation phase** of the global execution context:

1.  The JavaScript engine encounters the `function foo() { console.log("Hello"); }` declaration.
2.  It hoists the *entire* function (both its name `foo` and its definition) to the top of the global scope.

During the **execution phase**:

1.  The line `foo();` is executed. Since the `foo` function was fully hoisted in the creation phase, it is already defined and available.
2.  The `foo()` function is called, and `console.log("Hello");` is executed, printing "Hello" to the console.

---

Let's address the questions one by one.

## 13. What would be the result of the following code and why?
`foo(); var foo = function() { console.log("Hi"); }`

**Result:**

TypeError: foo is not a function

**Why:**

This scenario involves a **function expression** and `var` hoisting. Here's a breakdown of what happens during the JavaScript execution:

1.  **Creation Phase:**
    * The `var foo` declaration is hoisted to the top of its scope. At this point, `foo` is initialized with `undefined`. The assignment of the actual function to `foo` has *not* happened yet.

2.  **Execution Phase:**
    * The first line `foo();` is executed.
    * At this moment, `foo` holds the value `undefined` (from the hoisting in the creation phase).
    * Attempting to call `undefined` as a function (`undefined()`) results in a `TypeError: foo is not a function`.
    * The line `var foo = function() { console.log("Hi"); }` is then executed, which would assign the function to `foo`, but the error has already occurred.

---

## 14. How does hoisting impact debugging and code readability?

Hoisting, while a fundamental part of JavaScript, can significantly impact debugging and code readability, sometimes leading to unexpected behavior.

**Impact on Debugging:**

* **Unexpected `undefined` Values:** When `var` variables are used before their explicit declaration and initialization, they will evaluate to `undefined`. This can lead to bugs that are hard to trace if the developer isn't aware of hoisting and expects a value to be present.
    * *Debugging Challenge:* You might see `undefined` where you expect a value, and tracing back to the actual assignment might be complex if the codebase is large or declarations are far apart from their usage.
* **`ReferenceError` with `let` and `const` (TDZ):** While `let` and `const` are hoisted, they are in a Temporal Dead Zone (TDZ) until their declaration. Accessing them before declaration causes a `ReferenceError`, which is often clearer than `undefined` but can still be surprising to developers unfamiliar with the TDZ concept.
    * *Debugging Challenge:* Understanding why a variable is "not defined" when it clearly appears later in the code requires knowledge of the TDZ.
* **Function vs. Function Expression Errors:** The difference in hoisting between function declarations (fully hoisted) and function expressions (only the variable is hoisted) can lead to `TypeError` if a function expression is called before its assignment.
    * *Debugging Challenge:* It requires careful inspection to differentiate between how a function was defined (`function funcName()` vs `var funcName = function()`) to understand why it might not be callable at a certain point.

**Impact on Code Readability:**

* **Non-Sequential Logic:** Code that relies heavily on hoisting can appear to violate the principle of reading code top-down. Declarations might be scattered, making it harder for someone reading the code (including the original developer later on) to quickly grasp variable and function availability.
    * *Readability Challenge:* A developer might need to scan the entire scope to understand what variables and functions are available at any given point, rather than just looking at what has been declared above.
* **Potential for Errors:** While not strictly a readability issue, the potential for `undefined` values or `TypeError` due to misunderstanding hoisting can make code seem less robust and harder to reason about, even if it "works" in some cases.
* **Encourages Bad Practices (historically):** Before `let` and `const`, `var`'s hoisting behavior sometimes led to variables being declared much later than their first use, which is generally considered poor practice for maintainability.
    * *Readability Solution:* Modern JavaScript practices strongly encourage declaring variables as close as possible to their first use and utilizing `let` and `const` to avoid many of the pitfalls associated with `var`'s hoisting.

## 15. Can you prevent hoisting-related bugs? If yes, how?

Yes, hoisting-related bugs can be prevented by following these best practices:

- **Use `let` and `const` instead of `var`**  
  These are block-scoped and not initialized until their declaration is evaluated, which helps avoid unexpected `undefined` values.

- **Always declare variables and functions at the top of their scope**  
  This makes the hoisting behavior explicit and easier to reason about.

- **Initialize variables as close as possible to their first use**  
  This improves code clarity and reduces the risk of accessing uninitialized variables.

- **Enable strict mode (`'use strict'`)**  
  It catches more errors, including silent bugs related to hoisting and undeclared variables.

---

## 16. Why should developers be cautious with `var` due to hoisting?

Developers should be cautious with `var` because:

- **`var` is function-scoped**, not block-scoped, which can lead to confusing behavior inside loops and conditionals.
- **Variables declared with `var` are hoisted and initialized with `undefined`**, which may cause bugs when trying to access the variable before the intended declaration.
- Re-declaring the same `var` variable in the same scope is allowed and won't throw an error, which can lead to unintentional overwrites.

**Example:**

```js
console.log(x); // undefined
var x = 5;
```

This code doesn’t throw an error, but x is undefined, which may lead to logic bugs.

## 17. Does JavaScript hoist import and export statements? How does this differ from variables?

Yes, JavaScript hoists import and export statements, but in a different way from variables:

- Imports and exports are hoisted to the top of the module, but they must be declared at the top level and cannot be conditionally loaded.
- Accessing an import before it’s evaluated will throw a `ReferenceError`, not return `undefined` like `var`.

**Key Differences:**

| Feature                   | Variables (`var`)      | Imports/Exports           |
|---------------------------|-----------------------|--------------------------|
| Hoisted?                  | Yes                   | Yes                      |
| Initialized during hoisting? | `var`: Yes (with `undefined`) | No (TDZ applies)           |
| Access before declaration? | Returns `undefined`    | Throws `ReferenceError`   |
| Conditional declaration allowed? | Yes               | No (must be top-level)   |

**Example:**

```js
console.log(myValue); // ReferenceError
import { myValue } from './module.js';
```
Even though myValue is hoisted, it is not accessible before its declaration due to the temporal dead zone (TDZ).

## 18. Practical Example Where Hoisting Might Introduce Unexpected Behavior

Consider the following JavaScript code snippet:

```js
function showMessage() {
  console.log(message);
  var message = "Hello, world!";
}

showMessage();
```

### What happens?

- You might expect the output to be `"Hello, world!"`, but instead, it logs `undefined`.
- This happens because the declaration of `var message` is hoisted to the top of the function, but its initialization (`"Hello, world!"`) is not.
- So the code is interpreted like this behind the scenes:


```js
Copy
Edit
function showMessage() {
  var message;           // Declaration hoisted
  console.log(message);  // Logs 'undefined' because initialization hasn't happened yet
  message = "Hello, world!";
}
```
### Why is this unexpected?
- Developers often expect variables to hold their assigned values when accessed, but with var and hoisting, the variable exists but is uninitialized at the time of the console.log.

- This can cause bugs that are hard to trace, especially in larger functions or scripts.

### How to avoid this issue?
Use let or const instead of var. They are block-scoped and do not allow access before initialization (due to the Temporal Dead Zone), causing a clear error instead of silent undefined values.

Example with let:

```js
Copy
Edit
function showMessage() {
  console.log(message); // ReferenceError: Cannot access 'message' before initialization
  let message = "Hello, world!";
}

showMessage();
```