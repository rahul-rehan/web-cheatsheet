## 1. How can `new.target` be used to enforce the use of the `new` keyword?

You can check if `new.target` is `undefined` inside a function or constructor to determine if it was called without `new`. If `new.target` is `undefined`, you can throw an error or return a new instance to enforce the use of `new`.

```javascript
function Person(name) {
  if (!new.target) {
    throw new Error("Must use 'new' to call Person");
  }
  this.name = name;
}

new Person("Alice");  // Works fine
Person("Bob");        // Throws Error
```
## 2. Can `new.target` be used in arrow functions? Why or why not?

No, `new.target` cannot be used in arrow functions because arrow functions do not have their own `new.target` binding. They inherit `new.target` from the surrounding (enclosing) context, which means they cannot be used as constructors and do not support `new.target` internally.

## 3. What is the difference between using `this.constructor.name` and `new.target.name`?

- `this.constructor.name` refers to the constructor function of the current instance (the object’s prototype’s constructor). It depends on the instance's context and can be affected by changes to the prototype chain.
- `new.target.name` refers to the class or function that was directly invoked with the `new` keyword during instantiation. It reflects the *actual* constructor called, even if the code is running inside a parent class constructor.

Example:

```javascript
class Parent {
  constructor() {
    console.log("this.constructor.name:", this.constructor.name);
    console.log("new.target.name:", new.target.name);
  }
}

class Child extends Parent {}

new Child();
// Output:
// this.constructor.name: Child
// new.target.name: Child
```
In most cases, both are the same, but `new.target` is more reliable for detecting which constructor was directly called.
## 4. How is `new.target` helpful in frameworks or base class libraries?

`new.target` is useful in frameworks or base class libraries to enforce correct usage of constructors, such as ensuring that:

- A base class is not instantiated directly (enforcing abstract classes).
- A constructor is always called with the `new` keyword to avoid incorrect invocation.
- The actual class being instantiated is identified, which helps in creating flexible and reusable base classes or factory patterns.

By using `new.target`, libraries can throw errors or modify behavior depending on how classes are instantiated, improving robustness and developer experience.

## 5. Can you use `new.target` in class methods or static methods? Explain.

No, `new.target` is only defined inside constructor functions. It is not available inside regular class methods or static methods because those methods are not invoked with the `new` keyword.

- In **constructor functions**, `new.target` refers to the constructor that was called with `new`.
- In **class methods** (instance or static), the method is called on an instance or the class itself, not via `new`, so `new.target` is `undefined` there.

Attempting to use `new.target` in class methods or static methods will result in `undefined`.
## Best practices
## 1. When should you use `new.target` in real-world applications?

- To **enforce that constructors are called with `new`**, preventing accidental invocation as regular functions.
- To **implement abstract base classes** that should not be instantiated directly.
- To **detect which subclass is actually being instantiated** in complex inheritance hierarchies.
- To improve **error handling and debugging** by validating instantiation patterns.

## 2. What are some common mistakes when using `new.target`?

- Using `new.target` outside of constructors (e.g., in regular functions or class methods) where it is `undefined`.
- Forgetting to handle cases when `new.target` is `undefined`, leading to errors.
- Overusing `new.target` for logic better suited to other patterns, which can complicate code unnecessarily.
- Not considering inheritance, leading to incorrect assumptions about the instantiated class.

## 3. How can misuse of `new.target` lead to unexpected behavior in inheritance chains?

- If not properly checked, subclasses may bypass intended constructor logic or validations enforced using `new.target`.
- Overriding constructors without calling `super()` can interfere with `new.target` behavior.
- Misinterpreting `new.target` may cause incorrect identification of the instantiating class, breaking polymorphism.
- Incorrect use can cause confusing errors or security issues when restricting instantiation.

## 4. Is `new.target` widely supported in browsers and Node.js environments?

- Yes, `new.target` is supported in **modern browsers** (Edge 12+, Chrome 46+, Firefox 46+, Safari 10+).
- It is also supported in **Node.js versions 6.7.0 and later**.
- For older environments, transpilers like Babel may not fully support `new.target`, so polyfills or alternative patterns might be needed.
