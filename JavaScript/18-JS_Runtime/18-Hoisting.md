## 1. What is hoisting in JavaScript?

- **Hoisting** is JavaScript’s default behavior of **moving declarations** (variables and functions) to the top of their containing scope **during the creation phase** of the execution context.
- This means you can **use variables and functions before their actual declaration line** in the code without causing a ReferenceError (though behavior depends on declaration type).

## 2. Which types of declarations are hoisted in JavaScript?

- **Function declarations** are fully hoisted — the entire function body is hoisted.
- **Variables declared with `var`** are hoisted but only the declaration, **not the initialization**.
- **`let` and `const` declarations** are hoisted but are placed in a **Temporal Dead Zone (TDZ)** until their declaration is reached, so accessing them before declaration causes a ReferenceError.

## 3. Are variables declared with `var` hoisted? How?

- Yes, variables declared with `var` are hoisted to the top of their **function or global scope**.
- Only the **declaration** is hoisted, **not the assignment**.
- Before the assignment line, the variable exists but has the value `undefined`.

**Example:**

```js
console.log(a); // undefined, no ReferenceError
var a = 5;
console.log(a); // 5
```
#### This behaves like:

```js
var a;            // declaration hoisted
console.log(a);   // undefined (initialized to undefined)
a = 5;            // assignment happens here
console.log(a);   // 5
```

## 4. Are variables declared with `let` and `const` hoisted? Explain the difference from `var`.

- **Yes, `let` and `const` declarations are hoisted**, but differently from `var`.
- They are hoisted to the top of their **block scope**, but remain in the **Temporal Dead Zone (TDZ)** until their actual declaration line is executed.
- Accessing `let` or `const` variables **before their declaration causes a ReferenceError**.
- Unlike `var`, which is hoisted and initialized to `undefined`, `let` and `const` are **not initialized during hoisting**.

**Example:**

```js
console.log(x); // ReferenceError: Cannot access 'x' before initialization
let x = 10;

console.log(y); // ReferenceError: Cannot access 'y' before initialization
const y = 20;
```
#### In contrast, with `var`:

```js
console.log(z); // undefined (no error)
var z = 30;
```

## 5. Are function declarations hoisted? Provide an example.

- **Yes, function declarations are fully hoisted**, meaning both the function name and its entire body are moved to the top of their scope during the creation phase.
- This allows you to call the function **before** its declaration in the code without any errors.

**Example:**

```js
greet(); // Output: "Hello!"

function greet() {
  console.log("Hello!");
}
```
- The above code works because it is interpreted as if the function declaration appears at the top:

```js
function greet() {
  console.log("Hello!");
}

greet(); // Output: "Hello!"
```
- In contrast, function expressions (e.g., `const fn = function() {}`) are not hoisted in the same way.

## 6. Are function expressions hoisted? What happens when you try to call one before its definition?

- **Function expressions are not hoisted like function declarations.**
- When a function expression is assigned to a variable declared with `var`, only the variable declaration is hoisted (initialized as `undefined`), **not the function itself**.
- Calling a function expression **before its assignment** results in a **TypeError** because you're trying to call `undefined`.
- For `let` or `const` function expressions, accessing before declaration causes a **ReferenceError** due to the Temporal Dead Zone (TDZ).

**Example with `var`:**

```js
foo(); // TypeError: foo is not a function
var foo = function() {
  console.log("Hello");
};
```
## 7. What is the Temporal Dead Zone (TDZ) and how does it relate to hoisting?

- The **Temporal Dead Zone (TDZ)** is the time period between when a variable is hoisted and when it is actually declared and initialized in the code.
- Variables declared with `let` and `const` are hoisted but **cannot be accessed during the TDZ**.
- Attempting to access a variable in its TDZ results in a **ReferenceError**.

**Example:**

```js
console.log(x); // ReferenceError: Cannot access 'x' before initialization
let x = 5;
```
- The TDZ ensures variables are not used before they are properly initialized, helping prevent certain types of bugs.

## 8. What is the difference between `undefined` and `ReferenceError` in the context of hoisting?

| Situation                                           | Result          | Explanation                                                      |
|----------------------------------------------------|-----------------|------------------------------------------------------------------|
| Accessing a `var` variable before assignment       | `undefined`     | The variable declaration is hoisted and initialized to `undefined` during creation phase. |
| Accessing a `let` or `const` variable before declaration (inside TDZ) | `ReferenceError` | The variable is hoisted but not yet initialized; access is forbidden in the Temporal Dead Zone. |
| Accessing a completely undeclared variable         | `ReferenceError` | The variable does not exist in the current or any outer scope.  |

**Summary:**

- `undefined` means the variable exists but hasn't been assigned a value yet.
- `ReferenceError` means the variable either hasn't been initialized yet (TDZ) or doesn't exist at all.
