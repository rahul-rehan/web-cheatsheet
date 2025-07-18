## 1. How are static methods declared in ES6 class syntax?

Static methods are declared using the `static` keyword inside the class body, before the method name.

```javascript
class MyClass {
  static myStaticMethod() {
    console.log("This is a static method");
  }
}
```
## 2. Can static methods access instance-specific properties using `this`? Why or why not?

No, static methods cannot access instance-specific properties using `this` because `this` inside a static method refers to the class itself, not to any instance of the class.

## 3. Are static methods inherited by subclasses in ES6?

Yes, static methods are inherited by subclasses. Subclasses can call static methods defined in their parent class.
## 4. Provide an example of a class hierarchy with inherited static methods.

```js
class Parent {
  static greet() {
    return "Hello from Parent";
  }
}

class Child extends Parent {}

console.log(Child.greet()); // Output: "Hello from Parent"
```
## 5. Can you define static getters and setters? Show an example.

Yes, static getters and setters can be defined in a class. They allow controlled access to static properties.

```js
class Circle {
  static _pi = 3.14;

  static get pi() {
    return this._pi;
  }

  static set pi(value) {
    this._pi = value;
  }
}

console.log(Circle.pi); // 3.14
Circle.pi = 3.14159;
console.log(Circle.pi); // 3.14159
```
## 6. How can you define a utility/helper function as a static method?

Utility or helper functions that don't depend on instance data are ideal candidates for static methods. You define them inside the class using the `static` keyword.

```js
class MathUtils {
  static square(x) {
    return x * x;
  }
}

console.log(MathUtils.square(5)); // 25
```
