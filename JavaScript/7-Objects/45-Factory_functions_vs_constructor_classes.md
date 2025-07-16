## 1. How does `this` behave in factory functions vs constructor functions?

- **Factory Functions:**  
  Factory functions **do not use** the `this` keyword for object creation. Instead, they explicitly create and return a new object. Therefore, `this` inside a factory function behaves like a normal function’s `this` (often `undefined` in strict mode or the global object in non-strict mode), and is usually avoided.

- **Constructor Functions:**  
  Constructor functions rely on the `this` keyword to assign properties to the new object being created. When called with the `new` keyword, `this` refers to the new instance. Forgetting `new` can lead to `this` referring to the global object, causing bugs.

## 2. Can factory functions be used without the `new` keyword?

Yes, factory functions are designed to be called **without** the `new` keyword. They explicitly create and return a new object, so the `new` keyword is not required and often omitted.

Example:

```javascript
function createUser(name) {
  return {
    name,
    greet() {
      console.log(`Hi, I'm ${name}`);
    }
  };
}

const user = createUser('Alice'); // No 'new' needed
user.greet(); // Hi, I'm Alice
```
## 3. Why are factory functions sometimes more testable than class constructors?

- **Isolation:** Factory functions can easily create isolated instances without relying on the `new` keyword or prototype chains, making tests more predictable.
- **Encapsulation:** They support closures for private state, allowing easier testing of internal logic without exposing unnecessary details.
- **No reliance on `this`:** Since factory functions don’t depend on `this`, there are fewer pitfalls related to incorrect binding, reducing test complexity.
- **Simpler mocking:** Factory functions can be easily mocked or stubbed by replacing them with test doubles, improving test flexibility.

## 4. What are some limitations or drawbacks of factory functions compared to classes?

- **Memory usage:** Methods defined inside factory functions are recreated for every instance, which can lead to higher memory consumption compared to prototype-based methods shared by classes.
- **Lack of inheritance support:** Factory functions don’t natively support classical inheritance and the prototype chain, making some object-oriented patterns harder to implement.
- **Performance:** Due to method recreation, factory functions might be less performant when creating many instances with the same methods.
- **Less familiar syntax:** Some developers prefer the class syntax as it is more explicit and standardized in modern JavaScript.
