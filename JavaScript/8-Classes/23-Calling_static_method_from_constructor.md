## 1. Can a class constructor call a static method defined in the same class?

Yes, a class constructor can call a static method defined in the same class by referencing the class name inside the constructor.

## 2. Provide an example of calling a static method from a class constructor.

```js
class Example {
  constructor(value) {
    this.value = value;
    // Call the static method from the constructor using the class name
    Example.logValue(this.value);
  }

  static logValue(val) {
    console.log('Value is:', val);
  }
}

const obj = new Example(42);
// Output: Value is: 42
```
## 3. Can an instance method call a static method of its class? How?

Yes, an instance method can call a static method of its class by referencing the class name inside the instance method.

```js
class MyClass {
  static staticMethod() {
    console.log("Static method called");
  }

  instanceMethod() {
    // Call static method using class name
    MyClass.staticMethod();
  }
}

const obj = new MyClass();
obj.instanceMethod(); // Output: Static method called
```
## 4. How do you call a parent class’s static method from a child class?

You can call a parent class’s static method from a child class using the `super` keyword inside a static method of the child class.

```js
class Parent {
  static greet() {
    console.log("Hello from Parent");
  }
}

class Child extends Parent {
  static greet() {
    // Call parent static method
    super.greet();
    console.log("Hello from Child");
  }
}

Child.greet();
// Output:
// Hello from Parent
// Hello from Child
```
## 5. What is the value of `this` inside a static method?

Inside a static method, `this` refers to the class itself, not an instance of the class. This means you can use `this` to access other static methods or properties on the same class.

## 6. Is it better to access static methods via `ClassName.method()` or `this.constructor.method()` inside an instance method?

- Using `ClassName.method()` is straightforward but hardcodes the class name, which reduces flexibility if the class is extended.
- Using `this.constructor.method()` is more flexible because it dynamically refers to the actual class of the instance, supporting inheritance and subclasses better.

**Example:**

```js
class Parent {
  static staticMethod() {
    console.log("Static method");
  }
  
  instanceMethod() {
    // Better to use this.constructor.staticMethod() for flexibility
    this.constructor.staticMethod();
  }
}

class Child extends Parent {
  static staticMethod() {
    console.log("Child's static method");
  }
}

const c = new Child();
c.instanceMethod(); // Outputs: Child's static method
```

## Advance and Best Practices
## 1. When should you use static methods instead of instance methods?

Use static methods when the behavior or functionality does not depend on individual instance data but rather relates to the class as a whole. Examples include utility functions, factory methods, or operations that manage class-level data.

## 2. Can static methods have access to private static fields (via `#` syntax)?

Yes, static methods can access private static fields declared with `#` within the same class.

```js
class MyClass {
  static #privateStatic = 42;

  static getPrivateStatic() {
    return this.#privateStatic;
  }
}
```
## 3. Are static methods enumerable in the class?

No, static methods are **not enumerable**. They do not appear in `for...in` loops or `Object.keys()` on the class constructor.

## 4. How do you prevent name clashes between static and instance methods?

Since static and instance methods live on different objects (class constructor vs. prototype), you can use the same method names without conflict. However, to avoid confusion, choose distinct names or clearly document their purpose.

## 5. Can a static method return an instance of the class? Why would you do that?

Yes. Static methods often act as **factory methods**, returning new instances of the class. This is useful for creating objects with specific initialization or from alternate data formats.

```js
class Person {
  constructor(name) {
    this.name = name;
  }
  
  static fromJSON(json) {
    const data = JSON.parse(json);
    return new Person(data.name);
  }
}
```
## 6. What happens if you try to access a static method with `this.methodName()` from an instance?

If you call a static method using `this.methodName()` inside an instance method, it will result in an error because `this` refers to the instance, and static methods are not available on instances—they belong to the class constructor.

## 7. Is it possible to use static methods in mixins or utility classes?

Yes, static methods are commonly used in **mixins** or **utility classes** to provide reusable functionality that does not depend on instance state. They can be called directly on the class without creating an instance.

```js
const Mixin = Base => class extends Base {
  static helper() {
    console.log("Utility static method");
  }
};
```