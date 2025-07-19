## 1. How is `bind()` used to fix the `this` value inside a callback?

- When passing methods as callbacks, the original `this` context can be lost because the method is called as a plain function.
- Using `bind()` on the method creates a new function with `this` permanently set to the original object.
- This ensures that inside the callback, `this` refers to the correct object, avoiding common bugs related to context loss.

## 2. Example where `bind()` is used to ensure `this` refers to the correct object

```javascript
const obj = {
  name: 'Alice',
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

setTimeout(obj.greet, 1000); 
// Output after 1 second: "Hello, my name is undefined" (because `this` is lost)

setTimeout(obj.greet.bind(obj), 1000); 
// Output after 1 second: "Hello, my name is Alice"
```
- Without `bind()`, the callback loses its original `this` context and defaults to `undefined` (or the global object in non-strict mode).

- Using `bind(obj)` fixes `this` so the method correctly accesses `obj.name`.
## 3. Why is `bind()` often used in event handling or timers?

- In event handlers or timers, the callback function is often invoked with a different `this` context (e.g., the DOM element or the global object).
- Using `bind()` ensures that the callback retains the original object's `this` context, allowing it to access the object's properties and methods correctly.
- This prevents bugs caused by losing the intended `this` when the function is called asynchronously.

## 4. What problem does `bind()` solve when passing class methods as callbacks?

- Class methods rely on `this` to refer to the instance.
- When passing a class method as a callback (e.g., to an event listener or timer), the method can lose its class instance context.
- `bind()` fixes this by permanently binding the method's `this` to the class instance, ensuring the method behaves as expected when called later.
- Without `bind()`, `this` may become `undefined` or refer to an unintended object, causing errors.
## 5. Can you use `bind()` to pre-set arguments? What is this technique called?

- Yes, you can use `bind()` to pre-set one or more arguments of a function when creating the bound function.
- This technique is called **partial application**.
- Partial application allows you to create a new function with some arguments fixed in advance, making it easier to reuse functions with preset parameters.

#### Example of partial application using `bind()`:

```javascript
function greet(greeting, name) {
  console.log(`${greeting}, ${name}!`);
}

// Pre-set the first argument to 'Hello'
const sayHello = greet.bind(null, 'Hello');

sayHello('Alice'); // Output: Hello, Alice!
sayHello('Bob');   // Output: Hello, Bob!
```
