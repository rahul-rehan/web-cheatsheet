## 1. How do you define a global variable in JavaScript?

- A global variable is defined **outside of any function or block**, making it accessible throughout the entire program.
- Example:

```js
var globalVar = "I am global";
let anotherGlobal = 42;
const constantGlobal = true;
```
- In browsers, global variables declared with `var` become properties of the global `window` object, whereas `let` and `const` do not.

## 2. Are global variables accessible inside functions? Why?

- Yes, global variables are accessible inside functions because functions have access to variables declared in their outer (global) scope.
- This is due to JavaScript’s **lexical scoping**, where inner scopes can access variables from outer scopes.

**Example:**

```js
var globalVar = "Hello";

function greet() {
  console.log(globalVar); // Outputs: Hello
}

greet();
````

## 3. What are the risks of using global variables?

- **Name collisions:** Different parts of the code may unintentionally overwrite the same global variable.
- **Difficulty debugging:** Global variables can be changed from anywhere, making bugs harder to track.
- **Memory leaks:** Global variables persist for the lifetime of the program, potentially leading to higher memory usage.
- **Reduced modularity:** Heavy reliance on globals reduces code encapsulation and reusability.

## 4. Do var, let, and const create global variables differently when declared outside any function?

| Keyword | Global Variable Behavior                              |
|---------|-----------------------------------------------------|
| `var`   | Declares a global variable and adds it as a property to the global object (`window` in browsers). |
| `let`   | Declares a global variable but **does NOT** create a property on the global object.           |
| `const` | Same as `let`; declares a global variable without attaching it to the global object.            |

**Example:**

```js
var a = 1;
let b = 2;
const c = 3;

console.log(window.a); // 1
console.log(window.b); // undefined
console.log(window.c); // undefined
```