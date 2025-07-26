## 1. Which declarations (var, let, const) are function-scoped?

- Only **`var`** declarations are function-scoped.
- **`let`** and **`const`** are **block-scoped**, meaning they are limited to the block `{ ... }` in which they are declared.

## 2. Can variables declared inside a function be accessed outside it? Why or why not?

- No, variables declared inside a function **cannot be accessed outside** that function.
- This is because of **function scope**: variables declared inside a function exist only within that function's execution context and are not visible externally.

## 3. Provide an example of shadowing with function-scoped variables.

```js
var name = "Global";

function greet() {
  var name = "Local"; // Shadows the global 'name' variable inside this function
  console.log(name);  // Outputs: "Local"
}

greet();
console.log(name);    // Outputs: "Global"
```
- In this example, the `var name` inside `greet` shadows the global `name` variable, meaning inside `greet`, the local `name` takes precedence.