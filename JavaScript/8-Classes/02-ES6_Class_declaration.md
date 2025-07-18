## 1. How do you declare a class in ES6 using the `class` keyword?

In ES6, you can declare a class using the `class` keyword followed by the class name.

#### Example:

```javascript
class Person {
  // class body
}
```
## 2. What is the syntax for defining a constructor and methods in an ES6 class?

- The constructor is defined using the special method named `constructor` inside the class.
- Methods are defined as functions inside the class body without the `function` keyword.
- These methods are automatically added to the class prototype.

#### Example:

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
```
## 3. How do you create an instance of a class in ES6?

- You create an instance of a class using the `new` keyword followed by the class name and parentheses.
- The constructor method is automatically called during instantiation.

#### Example:

```javascript
const person1 = new Person('Alice', 30);
person1.greet(); // Output: Hello, my name is Alice
```
## 4. What is the difference between instance methods and static methods in ES6 classes?

- **Instance methods** are called on instances of the class (objects created by the class).
- **Static methods** are called on the class itself, not on instances.

```javascript
class Example {
  instanceMethod() {
    console.log('Called on instance');
  }

  static staticMethod() {
    console.log('Called on class');
  }
}

const obj = new Example();
obj.instanceMethod();      // Works
Example.staticMethod();    // Works
// obj.staticMethod();     // Error: not a function
```
## 5. Can you add getters and setters in ES6 class declarations? How?

Yes, ES6 classes support defining getters and setters using the `get` and `set` keywords inside the class body. These allow you to create computed properties that run code when accessed or assigned.

```javascript
class Person {
  constructor(name) {
    this._name = name;
  }

  // Getter for the 'name' property
  get name() {
    return this._name;
  }

  // Setter for the 'name' property
  set name(value) {
    this._name = value;
  }
}

const p = new Person('Alice');
console.log(p.name);  // Calls getter, outputs: Alice
p.name = 'Bob';       // Calls setter
console.log(p.name);  // Outputs: Bob
```
## 6. Are ES6 classes hoisted like function declarations?

No, ES6 classes are **not hoisted** like function declarations. You must declare a class before you use it; otherwise, you will get a ReferenceError.

```javascript
// This will throw ReferenceError because MyClass is not hoisted
const obj = new MyClass();

class MyClass {
  constructor() {
    console.log('Instance created');
  }
}
```
## 7. Provide an example of method overriding in a subclass using ES6 class syntax

```javascript
class Animal {
  speak() {
    console.log("Animal makes a sound");
  }
}

class Dog extends Animal {
  speak() {
    console.log("Dog barks");
  }
}

const dog = new Dog();
dog.speak(); // Output: Dog barks
```
Here, the `Dog` subclass overrides the `speak` method of the `Animal` superclass.
## 8. How do you implement inheritance using extends and super() in ES6 classes?

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a sound`);
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // Calls the parent class constructor
    this.breed = breed;
  }

  speak() {
    super.speak(); // Optionally call the parent method
    console.log(`${this.name} barks`);
  }
}

const dog = new Dog("Buddy", "Golden Retriever");
dog.speak();
// Output:
// Buddy makes a sound
// Buddy barks
```
- `extends` sets up the subclass to inherit from the superclass.

- `super()` calls the parent class constructor and must be called before using `this` in the subclass constructor.

- `super.methodName()` can be used to call methods from the parent class within the subclass.
## 9. What happens if you forget to call super() in a subclass constructor?

- In ES6 classes, if you have a subclass constructor, you **must** call `super()` before accessing `this`.
- Forgetting to call `super()` results in a **ReferenceError**: 

Must call super constructor in derived class before accessing 'this' or returning from derived constructor 
- This is because the parent class needs to initialize its part of the instance before the subclass can use `this`.

## 10. Can ES6 classes extend built-in objects like Array?

- Yes, ES6 classes **can extend** built-in objects such as `Array`, `Error`, `Date`, etc.
- This allows creating subclasses that inherit the behavior of native objects while adding custom functionality.
- Example extending `Array`:
```javascript
class MyArray extends Array {
  customMethod() {
    return 'Custom behavior';
  }
}

const arr = new MyArray(1, 2, 3);
console.log(arr.length);         // 3
console.log(arr.customMethod()); // Custom behavior
```
- However, extending some built-in objects can have caveats or browser compatibility issues in older environments.