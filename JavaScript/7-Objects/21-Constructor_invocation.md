## 1. What is the value of `this` inside a constructor function?

- Inside a constructor function, `this` refers to the **newly created object** instance.
- This object is implicitly returned by the constructor (unless the constructor explicitly returns another object).

## 2. How does `this` behave differently when a function is called with `new` vs without?

- **With `new`:**  
  - A new object is created, and `this` inside the constructor points to that new object.
  - The function acts as a constructor, returning the new object by default.

- **Without `new`:**  
  - `this` depends on the calling context:
    - In non-strict mode, it points to the global object (`window` in browsers).
    - In strict mode, it is `undefined`.
  - The function behaves like a regular function, not a constructor.

## 3. Can a constructor function return a custom object to override `this`?

- Yes, if a constructor explicitly returns an **object**, that object replaces the default `this` (the newly created instance).
- Example:
  ```js
  function Person() {
    this.name = "Default";
    return { name: "Custom" };
  }
  
  const p = new Person();
  console.log(p.name); // Outputs: "Custom"
    ```
## 4. What happens to `this` if a constructor returns a primitive value?

- If a constructor function returns a **primitive value** (e.g., a string, number, boolean), the return value is **ignored**.
- JavaScript will instead return the object referenced by `this` (i.e., the newly created instance).
- This ensures that constructors always return an object unless an alternative object is explicitly returned.

**Example:**
```js
function Person() {
  this.name = "Default";
  return 42; // primitive value is ignored
}

const p = new Person();
console.log(p.name); // Outputs: "Default"
```
