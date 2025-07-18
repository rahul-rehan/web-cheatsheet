## 1. How were classes implemented in JavaScript before ES6?

Before ES6, JavaScript did not have a native `class` syntax. Instead, classes were emulated using **constructor functions** and the **prototype** property. Developers created reusable object blueprints by defining functions that acted as constructors and attaching shared methods to their prototypes.

## 2. How do constructor functions work in JavaScript?

A **constructor function** is a regular function intended to be used with the `new` keyword. When called with `new`:

1. A new object is created.
2. The function’s `this` is bound to that new object.
3. The new object gets linked to the constructor’s `prototype`.
4. The function runs, often assigning properties to `this`.
5. The new object is returned automatically (unless another object is explicitly returned).

**Example:**

```javascript
function Person(name) {
  this.name = name;
}

const p = new Person("Alice");
console.log(p.name); // Alice
```
## 3. What is the role of the prototype property in pre-ES6 class emulation?

The `prototype` property in JavaScript plays a central role in emulating classes before ES6. When a constructor function is used to create an object, the newly created object is internally linked to the constructor's `prototype`.

This allows developers to:

- Define methods and shared properties once on the constructor’s `prototype`.
- Ensure all instances created by the constructor can access these shared methods.
- Promote memory efficiency by avoiding method duplication across instances.

#### Example:

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function () {
  console.log(`Hello, my name is ${this.name}`);
};

const p = new Person("Alice");
p.greet(); // Output: Hello, my name is Alice
```
In this example, `greet()` is shared across all `Person` instances via the prototype, rather than being recreated per instance.
## 4. Provide an example of creating a reusable type using a constructor function and prototype

```javascript
function Animal(name, species) {
  this.name = name;
  this.species = species;
}

Animal.prototype.describe = function () {
  return `${this.name} is a ${this.species}.`;
};

const dog = new Animal("Buddy", "dog");
console.log(dog.describe()); // Buddy is a dog.
```
## 5. How do you add methods to a custom type before ES6?

Before ES6, methods were added to custom types by attaching them to the constructor function's `prototype` property. This allows all instances of that type to share the same method, promoting memory efficiency.

#### Example:

```javascript
function Car(make, model) {
  this.make = make;
  this.model = model;
}

Car.prototype.getInfo = function () {
  return `${this.make} ${this.model}`;
};

const myCar = new Car("Toyota", "Camry");
console.log(myCar.getInfo()); // Output: Toyota Camry
```
By defining `getInfo` on `Car.prototype`, all `Car` instances can access the method without it being redefined for each object.
## 6. What are the drawbacks of using constructor functions and prototypes manually?

Using constructor functions and prototypes manually in pre-ES6 JavaScript has several drawbacks:

- **Boilerplate Code**: Requires more verbose syntax compared to the cleaner and more intuitive ES6 `class` syntax.
- **`this` Binding Confusion**: If the constructor is called without the `new` keyword, `this` may refer to the global object (in non-strict mode), leading to bugs.
- **Lack of Privacy**: There's no built-in support for private properties or methods. All data is publicly accessible.
- **Inheritance Complexity**: Implementing inheritance requires manually setting up the prototype chain and calling parent constructors.
- **Harder to Read and Maintain**: The prototype-based approach can be less intuitive and harder to follow, especially for developers coming from class-based languages.

While powerful, this approach is more prone to error and less readable than modern ES6 classes.
## 7. How do you check if an object was created using a constructor function?

You can check if an object was created using a specific constructor function by using the `instanceof` operator:

```javascript
function Person(name) {
  this.name = name;
}

const user = new Person("Alice");

console.log(user instanceof Person); // true
```
This checks whether the object’s prototype chain includes the constructor’s `prototype`.
## 8. What is the purpose of using `new` with a constructor function?

Using the `new` keyword with a constructor function serves several purposes:

1. **Creates a new empty object**: A fresh object is created to be initialized.
2. **Sets the prototype**: The new object’s internal `[[Prototype]]` is set to the constructor’s `prototype` property.
3. **Binds `this`**: Inside the constructor, `this` refers to the newly created object.
4. **Returns the new object**: Unless the constructor explicitly returns another object, the new one is returned by default.

#### Example:

```javascript
function Person(name) {
  this.name = name;
}

const user = new Person("Alice");
console.log(user.name); // Alice
```
Without `new`, the constructor function may not behave as expected, and `this` might refer to the global object (or `undefined` in strict mode), leading to bugs.