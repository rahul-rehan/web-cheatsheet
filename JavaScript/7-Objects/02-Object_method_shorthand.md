## 1. What is the shorthand syntax for defining methods in ES6 object literals?

- In ES6, you can define methods in object literals **without using the `function` keyword**.
- The method name is followed directly by parentheses and the function body.

#### Example:

```javascript
const obj = {
  greet() {
    console.log("Hi");
  }
};
```
## 2. Rewrite this method using shorthand syntax: `greet: function() { console.log("Hi"); }`.
Rewritten using ES6 shorthand syntax:

```javascript
greet() {
  console.log("Hi");
}
```
## 3. Is there any difference in behavior between regular and shorthand method syntax?

- **Mostly no difference:** Both create callable methods that behave similarly when invoked.
- **Key differences:**
  - Shorthand methods have a `[[HomeObject]]` internal slot, enabling the use of `super` within the method (important in inheritance scenarios).
  - Shorthand methods are **not constructible** — they cannot be used with the `new` operator, unlike regular function expressions.
- For typical method definitions and calls, the behavior is effectively the same.

> **Summary:** Shorthand syntax is preferred for cleaner code and better support for features like `super`.
## 4. Can shorthand method syntax be used for getters and setters?

- **Yes**, ES6 also provides shorthand syntax for defining getters and setters inside object literals.

#### Example:

```javascript
const obj = {
  _value: 10,

  get value() {
    return this._value;
  },

  set value(newValue) {
    this._value = newValue;
  }
};
```
## 5. Why is shorthand syntax preferred in modern JavaScript codebases?

- It results in **cleaner and more concise** code.
- Improves **readability** by reducing unnecessary boilerplate.
- Enables better **support for `super`** calls in methods, which is important for inheritance.
- Aligns with **modern JavaScript standards** and best practices.
- Encourages **consistent coding style** across projects.
## 6. Can arrow functions be used in object method shorthand syntax?

- **No**, arrow functions cannot be used with the shorthand method syntax.
- Arrow functions do **not** have their own `this`, `arguments`, or `super` bindings, so they are unsuitable for object methods that rely on these.
- If you want to use arrow functions as methods, you must assign them as regular properties:

```javascript
const obj = {
  method: () => {
    console.log(this); // `this` refers to the enclosing scope, not the object
  }
};
```
Generally, avoid using arrow functions as object methods when you need to access the object’s own properties via `this`.