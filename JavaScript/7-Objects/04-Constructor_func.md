## 1. What is a constructor function in JavaScript?

- A **constructor function** is a regular function used to create and initialize **objects**.
- When called with the `new` keyword, it:
  - Creates a new object.
  - Sets the constructor’s `this` to point to that new object.
  - Returns the new object implicitly (unless an object is explicitly returned).

## 2. How do you define and call a constructor function using the `new` keyword?

1. Define a function that sets properties on `this`.
2. Call the function using `new` to create a new instance.

#### Example:

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.greet = function() {
    console.log("Hello, my name is " + this.name);
  };
}

const person1 = new Person("Alice", 30);
person1.greet(); // Output: Hello, my name is Alice
```
## 3. What naming convention is typically used for constructor functions?

- Constructor functions are usually named using **PascalCase**.
- PascalCase means that each word starts with an uppercase letter and there are no underscores or hyphens.
- This convention helps differentiate constructor functions from regular functions and indicates they should be used with the `new` keyword.

#### Example:

```javascript
function Car(make, model) {
  this.make = make;
  this.model = model;
}

const myCar = new Car("Toyota", "Corolla");
```
## 4. What does the `new` keyword do internally when calling a constructor function?

When you call a constructor function with the `new` keyword, JavaScript performs the following internal steps:

1. Creates a new empty object: `{}`.
2. Sets the `this` value inside the constructor to the new object.
3. Links the new object’s prototype to the constructor’s `prototype` property.
4. Executes the constructor function code.
5. Returns the new object (unless the constructor returns a different object explicitly).

## 5. Can constructor functions take parameters? Give an example.

- Yes, constructor functions can take parameters to initialize object properties.

#### Example:

```javascript
function Animal(type, name) {
  this.type = type;
  this.name = name;
}

const pet = new Animal("Dog", "Buddy");
console.log(pet.type); // Output: Dog
console.log(pet.name); // Output: Buddy
```
## 6. What happens if you forget to use the `new` keyword when calling a constructor?

- If you call a constructor function **without `new`**:
  - In **non-strict mode**, `this` refers to the **global object**, and properties may unintentionally be assigned to it.
  - In **strict mode**, `this` is `undefined`, which will likely cause a runtime error.
  - The function will **not return a new object**, and the instance will not be created as expected.

#### Example:

```javascript
function User(name) {
  this.name = name;
}

const u1 = User("Alice");  // Forgot `new`
console.log(u1);           // Output: undefined
console.log(name);         // Output: Alice (added to global object)
```
✅ Always use `new` when calling a constructor to ensure proper object creation and avoid side effects.
## 7. How can constructor functions be used to create multiple instances with shared structure?

- Constructor functions allow you to create **multiple object instances** that share the same structure and behavior.
- Each instance created with the `new` keyword will have its own copy of the properties defined inside the constructor.
- Methods and shared properties can be placed on the constructor's **prototype** to avoid duplication and share functionality across all instances.

#### Example:

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// Shared method on the prototype
Person.prototype.greet = function() {
  console.log(`Hi, I'm ${this.name} and I'm ${this.age} years old.`);
};

// Create multiple instances
const alice = new Person("Alice", 30);
const bob = new Person("Bob", 25);

alice.greet(); // Output: Hi, I'm Alice and I'm 30 years old.
bob.greet();   // Output: Hi, I'm Bob and I'm 25 years old.
```
By using the prototype, all instances share the same method in memory, improving efficiency.