## 1. How is `this` determined when calling a method on an object?

- When a method is called on an object, `this` refers to the **object the method was called on** (the receiver).
- Example:
  ```js
  const obj = {
    name: "Alice",
    greet() {
      console.log(this.name);
    }
  };
  obj.greet(); // 'Alice' — here `this` refers to `obj`
    ```
## 2. What happens to `this` if a method is extracted and invoked independently?

- When a method is extracted from an object and invoked as a standalone function:
  - In **non-strict mode**, `this` defaults to the **global object** (`window` in browsers).
  - In **strict mode**, `this` becomes **`undefined`**.
- This causes the method to lose the original object context, often leading to bugs.


## 3. Provide an example where `this` loses its context when a method is assigned to a variable

```js
const obj = {
  name: "Alice",
  greet() {
    console.log(this.name);
  }
};

const greetFunc = obj.greet; // Method extracted from obj
greetFunc(); // Outputs: undefined (in strict mode), because `this` is no longer `obj`
```
- The method `greet` is called without an object, so `this` does not refer to `obj` anymore.