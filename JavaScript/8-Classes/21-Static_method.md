## 1. What is a static method in JavaScript?

A **static method** is a method defined on a class itself, rather than on instances of the class. Static methods are called on the class directly and cannot be accessed through instances.

## 2. How do you define a static method in a class?

You define a static method by using the `static` keyword inside the class body before the method name.

```js
class MyClass {
  static myStaticMethod() {
    console.log("This is a static method.");
  }
}
```
You call it like this:

```js
MyClass.myStaticMethod(); // Works
const obj = new MyClass();
obj.myStaticMethod(); // Error: obj.myStaticMethod is not a function
```
## 3. What is the difference between static and instance methods?

- **Static Methods**  
  - Defined on the class itself.  
  - Called directly on the class, not on instances.  
  - `this` inside a static method refers to the class.  
  - Used for utility or helper functions related to the class as a whole.

- **Instance Methods**  
  - Defined on the prototype and called on individual instances.  
  - `this` inside an instance method refers to the specific instance.  
  - Used to define behavior and properties unique to each object created from the class.
## 4. Can a static method be accessed from an instance of the class?

No, static methods cannot be accessed from an instance of the class. They are only accessible on the class itself.

## 5. Example of a static method and how to call it

```javascript
class MyClass {
  static greet() {
    return "Hello from static method!";
  }
}

// Calling static method on the class
console.log(MyClass.greet()); // Output: Hello from static method!

// Trying to call static method on an instance will result in an error
const instance = new MyClass();
// console.log(instance.greet()); // Error: instance.greet is not a function
```