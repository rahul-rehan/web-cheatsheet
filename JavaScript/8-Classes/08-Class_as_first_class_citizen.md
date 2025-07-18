## 1. What does it mean that classes are first-class citizens in JavaScript?

- Classes in JavaScript are treated like any other value (e.g., functions, objects).
- This means you can assign them to variables, pass them as arguments, return them from functions, and store them in data structures.

## 2. Can you assign a class to a variable or object property?

- Yes, classes can be assigned to variables or object properties just like functions or other values.

```js
const MyClass = class {
  greet() {
    return "Hello";
  }
};

const obj = {
  MyClassProp: class {
    greet() {
      return "Hi";
    }
  }
};
```
## 3. Can you return a class from a function? Provide an example.

- Yes, functions can return class definitions dynamically.

```js
function createClass(name) {
  return class {
    sayName() {
      return `My name is ${name}`;
    }
  };
}

const Person = createClass("Alice");
const p = new Person();
console.log(p.sayName()); // "My name is Alice"
```
## 4. Can you pass a class as an argument to a function?

Yes, classes in JavaScript are first-class citizens, so you can pass them as arguments to functions just like any other value.

## 5. Provide an example of dynamically generating a class inside a function.

```js
function extendClass(BaseClass) {
  return class extends BaseClass {
    greet() {
      return `Hello from extended class!`;
    }
  };
}

class Person {
  constructor(name) {
    this.name = name;
  }
  sayName() {
    return `My name is ${this.name}`;
  }
}

const ExtendedPerson = extendClass(Person);
const p = new ExtendedPerson("Alice");

console.log(p.sayName());  // "My name is Alice"
console.log(p.greet());    // "Hello from extended class!"
```
## 6. What are practical use cases for treating classes as first-class citizens?

- **Dynamic class creation:** You can create classes on the fly based on runtime conditions or inputs.
- **Higher-order functions:** Functions can accept classes as arguments or return new classes, enabling flexible patterns like mixins or decorators.
- **Dependency injection:** Pass different class implementations to functions or modules to swap behavior easily.
- **Factory patterns:** Return different classes from factory functions depending on configuration.
- **Metadata and reflection:** Store and manage classes as data for plugins, serialization, or ORM systems.

## 7. Can you store classes in arrays or collections like any other value?

Yes, classes can be stored in arrays, objects, maps, or any other collection since they are just values in JavaScript.

```js
class Cat {}
class Dog {}

const animals = [Cat, Dog];
const pets = new Map([
  ["feline", Cat],
  ["canine", Dog]
]);

// Instantiate dynamically
const MyPet = animals[0];
const petInstance = new MyPet();
```
