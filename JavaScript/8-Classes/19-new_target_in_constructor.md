## 1. How can `new.target` be used to implement abstract base classes in JavaScript?

`new.target` can be used inside a base class constructor to check if the class is being instantiated directly. If so, you can throw an error to prevent direct instantiation, effectively creating an abstract base class.

## 2. Example: Using `new.target` to prevent direct instantiation of a base class

```javascript
class AbstractBase {
  constructor() {
    if (new.target === AbstractBase) {
      throw new Error("Cannot instantiate AbstractBase directly");
    }
  }

  someMethod() {
    console.log("Method from AbstractBase");
  }
}

class Derived extends AbstractBase {
  constructor() {
    super();
    console.log("Derived class instantiated");
  }
}

const instance = new Derived(); // Works fine
const baseInstance = new AbstractBase(); // Throws Error: Cannot instantiate AbstractBase directly
```
## 3. How does `new.target` behave in a subclass constructor?

In a subclass constructor, `new.target` refers to the class that was *actually* instantiated, not necessarily the class where the constructor code is written. This means that even if you are inside a parent class constructor, `new.target` will point to the subclass if the subclass was instantiated.

## 4. What will `new.target.name` return inside a subclass constructor?

`new.target.name` returns the name of the class that was directly instantiated. For example, if a subclass is instantiated, `new.target.name` inside the parent constructor will return the subclass’s name.

## 5. Can `new.target` help identify which class was actually instantiated? How?

Yes, `new.target` allows you to detect at runtime which class was used with `new` to create the instance. This is useful for things like enforcing abstract base classes or changing behavior depending on the actual class instantiated.

```javascript
class Parent {
  constructor() {
    console.log(`Instantiated class: ${new.target.name}`);
  }
}

class Child extends Parent {}

new Parent(); // Logs: "Instantiated class: Parent"
new Child();  // Logs: "Instantiated class: Child"
