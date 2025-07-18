## 1. Can you extend built-in types like Array, Error, or Map in JavaScript?

Yes, in modern JavaScript (ES6 and later), you can extend built-in types such as `Array`, `Error`, `Map`, and others by using the `extends` keyword in class declarations.

## 2. What are the benefits of extending built-in types?

- You can add custom behavior or methods to built-in types.
- You can create specialized versions of built-in objects tailored to your application's needs.
- It allows you to maintain the original prototype chain and behavior while extending functionality.

## 3. Example: Creating a custom class that extends Array

```js
class CustomArray extends Array {
  sum() {
    return this.reduce((total, num) => total + num, 0);
  }
}

const arr = new CustomArray(1, 2, 3, 4);
console.log(arr.sum()); // Output: 10
console.log(arr instanceof Array); // true
```
## 4. What special handling is required when extending Error to create custom errors?

- When extending `Error`, you should call `super(message)` in the constructor to set the error message properly.
- To ensure the custom error has the correct name, you often need to explicitly set `this.name = 'CustomErrorName'`.
- Capturing the stack trace correctly may require using `Error.captureStackTrace(this, this.constructor)` in some environments (like Node.js).
- Without these steps, the custom error might not behave exactly like native errors (e.g., incorrect stack trace or name).

## 5. What are some caveats when extending built-in types in older JavaScript environments?

- In pre-ES6 or older environments, extending built-ins like `Array` or `Error` may not work as expected due to prototype chain limitations.
- The `instanceof` checks might fail or constructors might not initialize properly.
- Some older JavaScript engines do not support subclassing built-ins natively, leading to inconsistent behavior.
- Workarounds or polyfills are often necessary to simulate inheritance.

## 6. Are there performance considerations when extending built-in objects?

- Extending built-ins can sometimes have a minor performance overhead compared to using plain objects or factory functions.
- This is usually negligible in most applications but could matter in performance-critical code.
- Overuse of subclassing and complex inheritance chains might impact optimization by JavaScript engines.
- It is generally recommended to extend built-ins only when you need the specific functionality and benefits they provide.
## Best Practices and Pitfall
## 1. When should you prefer composition over inheritance in JavaScript?

- Prefer **composition** when you want to build complex functionality by combining simpler, reusable components rather than relying on a rigid class hierarchy.
- Composition offers better flexibility and avoids the tight coupling and fragility often introduced by deep inheritance chains.
- Use composition to share behavior across unrelated objects or when multiple behaviors need to be combined dynamically.
- Composition helps avoid issues like the “fragile base class problem” and promotes cleaner, more maintainable code.

## 2. How does ES6 class inheritance differ from prototypal inheritance?

- **ES6 class inheritance** uses the `class` and `extends` syntax to create subclass-superclass relationships, providing a more familiar and declarative syntax similar to classical OOP languages.
- Behind the scenes, ES6 classes still use JavaScript’s **prototypal inheritance**, meaning methods are inherited via the prototype chain.
- Prototypal inheritance can be done more flexibly by directly linking objects without classes or constructors.
- ES6 classes formalize inheritance with a clearer structure (constructor, super calls, etc.), while prototypal inheritance is more dynamic and less restrictive.
## 3. What are common mistakes developers make when working with extends and super?

- **Forgetting to call `super()`** in a subclass constructor before using `this`, which causes a ReferenceError.
- Calling `super()` incorrectly or multiple times inside a constructor.
- Misunderstanding that `super` refers to the parent class prototype, so using it incorrectly in static methods or outside class methods.
- Overriding methods without calling `super.method()` when needed, which can break expected behavior.
- Confusing instance methods with static methods and how `super` behaves differently in each context.

## 4. Why is it important to understand the prototype chain when dealing with inheritance?

- The prototype chain determines how properties and methods are looked up at runtime, affecting behavior and performance.
- Understanding it helps debug issues where inherited methods or properties are not found or unexpectedly overridden.
- It clarifies how `extends` and `super` work under the hood, showing that classes are syntactic sugar over prototype-based inheritance.
- Helps in designing efficient and correct inheritance hierarchies by knowing how objects delegate behavior to their prototypes.
