## 1. Why should arrow functions be avoided in DOM event handlers?

- Arrow functions **do not have their own `this`**, so inside an event handler, `this` does **not** refer to the DOM element that triggered the event.
- This breaks the typical behavior expected in event handlers where `this` points to the element receiving the event.
- As a result, arrow functions can make it harder to access or manipulate the event target directly inside the handler.

## 2. What does `this` refer to inside an arrow function used as an event handler?

- Inside an arrow function used as an event handler, `this` is lexically inherited from the **enclosing scope** where the arrow function was defined.
- It **does not** refer to the DOM element that triggered the event.
- Often, this means `this` could refer to the global object (`window`) or be `undefined` in strict mode, depending on where the arrow function is defined.
## 3. Example where using an arrow function in an event listener causes incorrect behavior

```javascript
const button = document.querySelector('button');

button.addEventListener('click', () => {
  console.log(this); // 'this' does NOT refer to the button element
  // Output might be Window or undefined (in strict mode)
});
```
- Here, the arrow function inherits `this` from the enclosing scope (likely the global scope), not from the button element that triggered the event.

- This prevents access to properties or methods on the button via `this`.
## 4. How can using a regular function fix this binding in an event handler?
```javascript
const button = document.querySelector('button');

button.addEventListener('click', function() {
  console.log(this); // 'this' correctly refers to the button element
});
```
- Using a **regular function** gives the event handler its own `this` context, which by default points to the element that fired the event (e.g., the button element).

- This allows access to element properties and methods via `this` inside the handler.
