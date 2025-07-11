## 1. What is function hoisting in JavaScript?

**Function hoisting** is a JavaScript behavior where **function declarations** are moved ("hoisted") to the top of their scope before code execution. This means you can call a function **before** its actual declaration in the code.

## 2. Are function declarations hoisted? What about function expressions?

- ✅ **Function declarations** are **hoisted completely** — both their name and body are moved to the top of their scope.
  
  ```javascript
  sayHello();  // Output: Hello!

  function sayHello() {
    console.log("Hello!");
  }
  ```
- ❌ Function expressions (including arrow functions) are **not hoisted** in the same way.  
Only the variable declaration is hoisted, **not the function definition**.

    ```javascript
    greet();  // TypeError: greet is not a function

    var greet = function() {
    console.log("Hi!");
    };
    ```
## 3. What will happen if you call a function before it's defined using a declaration?

If you call a function **before its declaration** and it was declared using a **function declaration**, the call will work because the function is hoisted.

#### Example:

```javascript
sayHello();  // Output: Hello!

function sayHello() {
  console.log("Hello!");
}
```
If you use a function expression or arrow function, calling it before its definition will throw an error.

```javascript
sayHi();  // TypeError: sayHi is not a function

var sayHi = () => {
  console.log("Hi!");
};
```
## 4. What will happen if you call a function before it's defined using a function expression?

If you call a function **before** it is defined using a **function expression**, you will get an error:

- The variable declaration is hoisted but **not the function assignment**.
- Calling the function before assignment results in a **TypeError** because the variable is `undefined` at that point.

```javascript
greet();  // TypeError: greet is not a function

var greet = function() {
  console.log("Hello!");
};
```
## 5. Are arrow functions hoisted in the same way as function declarations?

No, **arrow functions** are **not hoisted** like function declarations.

- Arrow functions are typically assigned to variables.
- Only the variable declaration is hoisted (initialized as `undefined`), **not the arrow function itself**.
- Calling an arrow function before its assignment will result in a **TypeError**.

```javascript
sayHi();  // TypeError: sayHi is not a function

var sayHi = () => {
  console.log("Hi!");
};
```
## 6. How does hoisting affect variable and function declarations in the same scope?

- **Function declarations** are hoisted **before** variable declarations.
- If a variable and a function share the same name, the **function declaration takes precedence** during hoisting.
- However, if the variable is later assigned a value, it will **overwrite** the function.

```javascript
console.log(foo);  // Output: function foo() {}

var foo = "bar";

function foo() {
  console.log("I'm a function");
}

console.log(foo);  // Output: "bar"
```
**Explanation:**

- The function `foo` is hoisted first.
- The variable `foo` declaration is hoisted but **not** its assignment.
- When the assignment `foo = "bar"` runs, it overwrites the function `foo`.
