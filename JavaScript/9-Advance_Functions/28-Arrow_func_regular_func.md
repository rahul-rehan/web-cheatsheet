## 1. What are the key differences between arrow functions and regular functions?

- **Syntax:** Arrow functions have a shorter, more concise syntax.
- **`this` Binding:** Arrow functions do **not** have their own `this`; they inherit `this` from the enclosing scope (lexical `this`).
- **`arguments` Object:** Arrow functions do not have their own `arguments` object.
- **Constructors:** Arrow functions **cannot** be used as constructors and will throw an error if used with `new`.
- **Methods:** Arrow functions are not suitable for defining object methods that rely on their own `this`.

## 2. How do arrow functions handle the `this` keyword compared to regular functions?

- **Arrow functions:** Use **lexical scoping** for `this`, meaning `this` is inherited from the surrounding (parent) scope at the time of the arrow function's definition.
- **Regular functions:** Have their own `this` context which depends on how the function is called (dynamic `this`).

## 3. Can arrow functions be used as constructors? Why or why not?

- **No**, arrow functions **cannot** be used as constructors.
- They lack their own `this` binding and the internal `[[Construct]]` method necessary to work with `new`.
- Attempting to use `new` with an arrow function will throw a **TypeError**.
## 4. Do arrow functions have a prototype property?

- **No**, arrow functions do **not** have a `prototype` property.
- This is because they are not meant to be used as constructors or with the `new` keyword.

## 5. Can you use `arguments` inside arrow functions? Why or why not?

- Arrow functions **do not** have their own `arguments` object.
- Instead, they inherit `arguments` from the enclosing (parent) function's scope.
- If used at the top level or outside a regular function, `arguments` is not available in arrow functions.

## 6. When should you avoid using arrow functions?

- When you need a function to have its own `this` context, such as:
  - Defining object methods that rely on `this`.
  - Using functions as constructors (with `new`).
- When you need access to the function's own `arguments` object.
- When you require dynamic `this` binding (e.g., event handlers needing specific context).
## 7. How does lexical scoping of `this` in arrow functions impact event handlers or callbacks?

- Because arrow functions use **lexical scoping** for `this`, the value of `this` inside an arrow function is inherited from the surrounding context where the function is defined—not from how or where it is called.
- In **event handlers or callbacks**, this means:
  - The `this` inside an arrow function will **not** refer to the event target or the object triggering the callback.
  - Instead, it refers to the **enclosing lexical scope's** `this`.
- This behavior is useful to **avoid having to explicitly bind** the function or use variables like `self = this` to maintain context.
  
#### Example:

```javascript
const button = document.querySelector('button');
const obj = {
  id: 42,
  handleClick: () => {
    console.log(this.id); // 'this' does NOT refer to obj here; likely undefined or window object
  }
};

button.addEventListener('click', obj.handleClick);
```
- In this example, `this.id` inside the arrow function is not `42` because `this` is lexically bound, not dynamically set by the event.

- To correctly reference the object, use a regular function or explicitly bind the method.

## Arrow Functions – Limitations and Pitfalls
## 1. Why are arrow functions not suitable for every use case in JavaScript?

- Arrow functions **lack their own `this`**, which makes them unsuitable in cases where a dynamic or specific `this` context is needed (e.g., object methods, event handlers that rely on `this`).
- They **cannot be used as constructors** because they do not have a `prototype` property or internal `[[Construct]]` method.
- Arrow functions **do not have their own `arguments` object**, limiting their use in functions that need to handle variable numbers of arguments.
- They can sometimes make debugging harder due to implicit returns and less explicit context.

## 2. What are the key limitations of arrow functions compared to regular functions?

- **No own `this` binding:** They inherit `this` lexically.
- **No `arguments` object:** Cannot access their own `arguments`.
- **Cannot be used as constructors:** Will throw an error if used with `new`.
- **No `prototype` property:** Cannot be used to define prototype methods.
- **Less suited for object methods:** Because they don't have their own `this`, they don't work well as methods that rely on dynamic context.
