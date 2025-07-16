## 1. What is an object method in JavaScript?

- An **object method** is a function that is a property of an object.
- It allows the object to perform actions or behaviors related to its data.
- Methods can access and manipulate the object’s properties using `this`.

## 2. How do you define a method inside an object literal?

- You define a method by assigning a function as a value to a property inside the object.
- ES6 also allows a shorthand syntax to define methods without the `function` keyword.

#### Example (traditional and shorthand syntax):

```javascript
const obj = {
  // Traditional function expression
  method1: function() {
    console.log("Hello from method1");
  },

  // ES6 method shorthand
  method2() {
    console.log("Hello from method2");
  }
};
```
## 3. Provide an example of an object with two methods: `greet` and `farewell`

```javascript
const person = {
  name: "Alice",

  greet() {
    console.log("Hello, " + this.name + "!");
  },

  farewell() {
    console.log("Goodbye, " + this.name + "!");
  }
};

person.greet();    // Output: Hello, Alice!
person.farewell(); // Output: Goodbye, Alice!
```
Both `greet` and `farewell` are methods that access the object's `name` property using `this`.
## 4. Can object methods call other methods within the same object? How?

- Yes, object methods can call other methods of the same object using the `this` keyword.
- `this` refers to the current object, allowing access to its other methods.

#### Example:

```javascript
const calculator = {
  add(a, b) {
    return a + b;
  },

  doubleSum(a, b) {
    // Call another method using `this`
    return this.add(a, b) * 2;
  }
};

console.log(calculator.doubleSum(3, 4)); // Output: 14
```
## 5. How can you dynamically add a method to an existing object?

- You can add a method to an object at any time by assigning a function to a new property on that object.

#### Example:

```javascript
const obj = {};

// Dynamically add a method
obj.sayHello = function() {
  console.log("Hello!");
};

obj.sayHello(); // Output: Hello!
```
## 6. How do you delete a method from an object?

- Use the `delete` operator to remove a method (property) from an object.

#### Example:

```javascript
const obj = {
  greet() {
    console.log("Hi!");
  }
};

obj.greet(); // Output: Hi!

delete obj.greet;

console.log(obj.greet); // Output: undefined
```
