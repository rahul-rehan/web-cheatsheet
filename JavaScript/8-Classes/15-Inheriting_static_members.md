## 1. Are static methods and properties inherited when using `extends`?

Yes, static methods and properties are inherited by subclasses when using `extends`. The subclass can access and even override static members defined in the parent class.

## 2. How do you define a static method or property in a class?

You define static methods and properties using the `static` keyword inside the class body.

```js
class MyClass {
  static staticMethod() {
    return 'I am static';
  }

  static staticProperty = 'Static value';
}
```
## 3. Example of inheriting a static method from a parent class

```js
class Parent {
  static greet() {
    return 'Hello from Parent';
  }
}

class Child extends Parent {}

console.log(Child.greet()); // Output: "Hello from Parent"
```
In this example, the `Child` class inherits the static method `greet` from the `Parent` class and can call it directly without creating an instance.
## 4. Can a subclass override a static method?

Yes, a subclass can override a static method by defining a static method with the same name.

## 5. How can you call a static method of a parent class from a subclass?

You can call a static method of the parent class using `super.methodName()` inside the subclass.

## 6. What is the difference between instance and static members in the context of inheritance?

- **Instance members** belong to individual instances of a class and are accessed via the object created from the class.
- **Static members** belong to the class itself and are accessed directly on the class, not on instances. Static members are inherited by subclasses but are not accessible via instances.

```js
class Parent {
  static staticMethod() {
    return 'Parent static method';
  }

  instanceMethod() {
    return 'Parent instance method';
  }
}

class Child extends Parent {
  static staticMethod() {
    return 'Child static method';
  }

  callParentStatic() {
    return super.constructor.staticMethod(); // Calls Parent static method
  }
}

console.log(Child.staticMethod()); // "Child static method"

const childInstance = new Child();
console.log(childInstance.instanceMethod()); // "Parent instance method"
console.log(childInstance.callParentStatic()); // "Parent static method"
```