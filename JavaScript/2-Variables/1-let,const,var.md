# JavaScript Variables: `var`, `let`, and `const`

## 1. What is the difference between `var`, `let`, and `const` in JavaScript?

| Feature             | `var`                            | `let`                          | `const`                         |
|---------------------|----------------------------------|--------------------------------|---------------------------------|
| Scope               | Function-scoped                  | Block-scoped                   | Block-scoped                    |
| Hoisting            | Yes (initialized as `undefined`) | Yes (but not initialized)      | Yes (but not initialized)       |
| Redeclaration       | Allowed                          | Not allowed                    | Not allowed                     |
| Reassignment        | Allowed                          | Allowed                        | Not allowed                     |
| Temporal Dead Zone  | No                               | Yes                            | Yes                             |

---

## 2. When were `let` and `const` introduced in JavaScript?

Both `let` and `const` were introduced in **ECMAScript 6 (ES6)**, which was released in **2015**.

---

## 3. What is variable hoisting, and how does it differ for `var`, `let`, and `const`?

**Hoisting** is JavaScript’s behavior of moving variable and function declarations to the top of their scope before code execution.

- **`var`** is hoisted and initialized with `undefined`. You can use it before it's declared (though it's not recommended).
- **`let` and `const`** are hoisted but **not initialized**. Accessing them before declaration causes a **ReferenceError** due to the **Temporal Dead Zone (TDZ)**.

### Example:
```javascript
console.log(a); // undefined
var a = 5;

console.log(b); // ReferenceError
let b = 10;
```

## 4. Can you reassign a value to a `const` variable? Why or why not?

No, you **cannot reassign** a value to a variable declared with `const`. This is because `const` creates a **read-only reference** to a value. Once the variable is initialized, its binding cannot be changed to reference a different value or object. Attempting to reassign will result in a `TypeError`.

```js
const x = 10;
x = 20; // TypeError: Assignment to constant variable.
```

## 5. What does it mean when we say const creates an immutable binding?
Saying const creates an immutable binding means that the variable identifier cannot be reassigned to a different value or reference. However, the value itself is not necessarily immutable. For primitive types (like numbers or strings), the value is immutable by nature. For objects and arrays, the contents can still be changed (mutated), but the binding to the object reference cannot.

Example:
```js
const arr = [1, 2, 3];
arr.push(4); // This is allowed, the array content changes
arr = [5, 6]; // Not allowed, reassigning the variable causes error
```

## 6. What is the Temporal Dead Zone (TDZ) in JavaScript?
The Temporal Dead Zone (TDZ) refers to the time period between the start of a block scope and the point where a let or const variable is declared and initialized. During this period, the variable exists but cannot be accessed; accessing it will throw a ReferenceError.

This happens because let and const declarations are hoisted but not initialized until their actual declaration line is executed. The TDZ helps catch errors where variables are used before initialization.

Example:

```js
Copy
Edit
{
  console.log(a); // ReferenceError: Cannot access 'a' before initialization
  let a = 5;
}
```

# Summary

| Concept                 | Description                                                      |
|-------------------------|------------------------------------------------------------------|
| const reassignment      | Not allowed; `const` creates a read-only binding to a value     |
| Immutable binding       | Variable binding can't be changed; value may be mutable if object|
| Temporal Dead Zone (TDZ)| Period before `let`/`const` initialization where access throws error|


## 7. Why is `var` considered function-scoped, while `let` and `const` are block-scoped?

- **`var` is function-scoped** because its scope is limited to the entire function in which it is declared, or global if declared outside any function. It does not recognize block boundaries such as loops or conditionals.
  
- **`let` and `const` are block-scoped**, meaning their scope is limited to the nearest enclosing block (anything wrapped in `{}`), such as loops, conditionals, or code blocks. This allows better control over variable visibility and avoids issues related to `var`'s hoisting and scope leakage.

---

## 8. Example showing scoping differences between `var`, `let`, and `const`

```js
function testScope() {
  if (true) {
    var a = "var scoped";
    let b = "let scoped";
    const c = "const scoped";
  }

  console.log(a); // Works: "var scoped" (function scoped)
  console.log(b); // Error: b is not defined (block scoped)
  console.log(c); // Error: c is not defined (block scoped)
}

testScope();
```

- `a` is accessible outside the `if` block because `var` is function-scoped.

- `b` and `c` are not accessible outside the block due to block scoping.

---

## 9. Can a `const` object have its properties modified? Explain with an example.

Yes, a `const` object cannot be reassigned to a different object, but its properties can be modified because the binding to the object reference is immutable, not the object itself.

### Example:

```js
const person = {
  name: "Alice",
  age: 25
};

// Modifying properties is allowed
person.age = 26;
person.city = "New York";

console.log(person);
// Output: { name: "Alice", age: 26, city: "New York" }

// Reassigning the whole object is NOT allowed
person = { name: "Bob" }; // TypeError: Assignment to constant variable.
```
# Summary

| Concept                | Explanation                                                   |
|------------------------|---------------------------------------------------------------|
| var scoping            | Function-scoped, ignores block boundaries                     |
| let and const          | Block-scoped, limited to nearest `{}` block                   |
| const object mutability| Binding is immutable, but object properties can be changed    |


## 10. What happens if you try to redeclare a `let` variable in the same scope?

If you try to **redeclare** a `let` variable within the same scope, JavaScript will throw a **SyntaxError**. This is because `let` does not allow multiple declarations of the same variable in the same block scope.

```js
let x = 10;
let x = 20; // SyntaxError: Identifier 'x' has already been declared
```

## 11. Can you declare a variable without initializing it using `let`, `const`, or `var`?

- **`let` and `var`:** Yes, you can declare a variable without initializing it. The variable will be initialized with the value `undefined`.

```js
let a;
console.log(a); // undefined

var b;
console.log(b); // undefined
```

- **const:** No, you cannot declare a `const` variable without initializing it. `const` requires an initializer at the time of declaration.

```js
const c; // SyntaxError: Missing initializer in const declaration
```

## 12. Which declaration type (`var`, `let`, `const`) is preferred in modern JavaScript and why?

In modern JavaScript, **`let` and `const`** are preferred over `var`.

- **`const`** is generally the preferred choice when you want to declare variables whose values should not be reassigned. It helps prevent accidental reassignment and makes the code easier to reason about.

- **`let`** is used when you need a variable whose value can change over time (reassignment is required).

### Reasons for preferring `let` and `const` over `var`:

1. **Block scoping:** Unlike `var` which is function-scoped, `let` and `const` are block-scoped. This prevents common bugs related to variable hoisting and scope leakage.

2. **Temporal Dead Zone (TDZ):** `let` and `const` help catch errors by disallowing access to variables before they are declared.

3. **Readability and maintainability:** Using `const` makes it clear which variables are intended to remain constant, improving code clarity.

### Summary:

| Declaration | Use Case                          | Scope        | Reassignment Allowed? |
|-------------|---------------------------------|--------------|----------------------|
| `var`       | Legacy code or function-scoped  | Function     | Yes                  |
| `let`       | Variables with changing values  | Block        | Yes                  |
| `const`     | Variables that don't reassign   | Block        | No                   |

---

**Best practice:**  
- Use `const` by default.  
- Use `let` only when reassignment is needed.  
- Avoid using `var` in new code.


## 13. What kind of errors occur if `let` or `const` variables are accessed before declaration?

Accessing `let` or `const` variables **before their declaration** results in a **ReferenceError** due to the **Temporal Dead Zone (TDZ)**. During the TDZ—the time from the start of the block until the variable is declared—the variable exists but cannot be accessed.

```js
console.log(x); // ReferenceError: Cannot access 'x' before initialization
let x = 5;
```

## 14. How do variable declarations behave inside loops (e.g., for loop) when declared with `var` vs `let`?

### `var` inside loops:

- Variables declared with `var` are **function-scoped** or globally scoped, **not block-scoped**.
- In a `for` loop, the **same single `var` variable** is reused in every iteration.
- This can cause unexpected behavior, especially with closures.

```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); 
}
// Output after 100ms: 3, 3, 3
```

### `let` inside loops:

- Variables declared with `let` are **block-scoped**.
- In a `for` loop, a **new binding** is created for each iteration.
- This preserves the loop variable’s value for each iteration and works well with closures.

```js
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// Output after 100ms: 0, 1, 2
```

### Summary

| Aspect                    | `var` Behavior                               | `let` Behavior                                   |
|---------------------------|----------------------------------------------|-------------------------------------------------|
| Access before declaration  | No error, value is `undefined` (hoisting)   | ReferenceError due to Temporal Dead Zone (TDZ)  |
| Scope inside loops         | Function/global scope, same variable reused | Block scope, new variable per iteration          |
| Closure behavior in loops  | Common source of bugs (all callbacks get last value) | Correctly captures iteration value               |

## 15. Can you use `let` or `const` to declare global variables? How does that differ from `var`?

- Yes, you can declare global variables using `let` or `const` by defining them outside any function or block.
- **Difference from `var`:**
  - Variables declared with `var` in the global scope become properties of the global object (`window` in browsers), but `let` and `const` **do not**.
  - `let` and `const` are **block-scoped**, while `var` is **function-scoped**.
  - `let` and `const` declarations are not hoisted in the same way as `var` and do not allow access before initialization (Temporal Dead Zone).

## 16. What are the implications of using `var` in modern JavaScript development?

- `var` is function-scoped and can cause unexpected bugs due to hoisting and scope leakage.
- It allows redeclaration and can overwrite variables unintentionally.
- Its global variables attach to the global object, which can lead to conflicts.
- Modern best practices discourage `var` usage in favor of `let` and `const` to improve readability, maintainability, and reduce bugs.

## 17. In what scenarios would you prefer using `const` over `let`, and vice versa?

- Use **`const`** when:
  - You want to declare variables whose reference should not change (constants).
  - It improves code clarity and intent by signaling immutability.
  - For objects and arrays, `const` prevents reassignment, but their contents can still be mutated.
- Use **`let`** when:
  - The variable value needs to be reassigned or updated later.
  - You require block-scoped variables that can change, e.g., loop counters or conditional reassignments.

## 18. What are the best practices for variable declarations in JavaScript?

- Prefer **`const`** by default; only use **`let`** if reassignment is needed.
- Avoid using `var` to prevent scope and hoisting issues.
- Use meaningful, descriptive variable names.
- Declare variables as close as possible to their first use.
- Use block scope to limit variable lifetime and avoid global pollution.
- Initialize variables when declaring to avoid undefined values.

## 19. What will be the output of the following code and why?

```js
console.log(a);
var a = 10;
```
Output:
```javascript
undefined
```
### Explanation for `var a`

The variable `a` is declared using `var`, which is hoisted to the top of its scope.

During hoisting, the declaration is moved to the top, but the assignment (`a = 10`) stays in place.

So effectively, the code behaves like:

```js
var a;
console.log(a); // undefined
a = 10;
```
Since a is declared but not yet assigned when console.log runs, it outputs undefined instead of throwing an error.

## 20. What will be the output of the following code and why?

```js
console.log(b);
let b = 20;
```
Output:
```js
ReferenceError: Cannot access 'b' before initialization
```
### Explanation:

- The variable `b` is declared with `let`, which is hoisted but **not initialized** during hoisting.
- Variables declared with `let` reside in the **Temporal Dead Zone (TDZ)** from the start of the block until their declaration is processed.
- Accessing `b` before its declaration throws a `ReferenceError`.
- Therefore, `console.log(b)` runs before `b` is initialized, causing the error.

