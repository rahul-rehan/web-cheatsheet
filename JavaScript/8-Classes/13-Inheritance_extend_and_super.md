## 1. What is the purpose of the `extends` keyword in JavaScript?

The `extends` keyword is used in JavaScript to create a class that is a child of another class. It sets up the prototype chain so that the subclass inherits methods and properties from the parent class.

## 2. How do you inherit from another class using `extends`?

To inherit from another class, you use the `extends` keyword when defining your subclass. Here's a basic example:

```js
class Animal {
  speak() {
    console.log("Animal speaks");
  }
}

class Dog extends Animal {
  bark() {
    console.log("Dog barks");
  }
}

const d = new Dog();
d.speak(); // Inherited from Animal
d.bark();  // Defined in Dog
```
## 3. What is the role of the `super` keyword in a subclass constructor?

The `super` keyword is used to call the constructor of the parent class. It must be called before using `this` in the subclass constructor to properly initialize the inherited properties.

Example:

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // Calls the parent class constructor
    this.breed = breed;
  }
}
```
If `super()` is not called before accessing `this`, JavaScript will throw a reference error.
## 4. What happens if you forget to call `super()` in a subclass constructor?

If you forget to call `super()` in a subclass constructor and try to use `this`, JavaScript will throw a `ReferenceError`. This is because the parent class constructor must be called first to properly initialize the `this` context in the subclass.

## 5. How do you call a method from the parent class using `super`?

You can call a method from the parent class inside a subclass method by using `super.methodName()`. This allows you to reuse or extend the behavior of the parent class method.

Example:
```js
class Animal {
  speak() {
    console.log("Animal speaks");
  }
}

class Dog extends Animal {
  speak() {
    super.speak(); // Calls the parent class method
    console.log("Dog barks");
  }
}
```
## 6. Can `super` be used outside of a constructor or method?

No, `super` can only be used inside constructors or methods of a subclass. Using `super` outside of these contexts will result in a syntax error.

## 7. Provide an example of class inheritance using `extends` and `super`.

```js
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // Call parent constructor
    this.breed = breed;
  }

  speak() {
    super.speak(); // Call parent method
    console.log(`${this.name} barks.`);
  }
}

const dog = new Dog("Buddy", "Golden Retriever");
dog.speak();
// Output:
// Buddy makes a noise.
// Buddy barks.
```
