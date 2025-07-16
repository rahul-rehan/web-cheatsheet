## 1. What is the constructor/prototype pattern in JavaScript?

- The **constructor/prototype pattern** is a common way to create multiple objects with shared structure and behavior.
- A **constructor function** initializes object-specific properties.
- Methods and shared properties are defined on the **constructor's prototype** so all instances share them without duplicating.

## 2. How does the constructor/prototype pattern enable inheritance and reuse?

- By placing methods on the constructor's prototype, all instances inherit those methods via the prototype chain.
- This avoids creating duplicate methods for each instance, saving memory and enabling consistent behavior.
- You can also create inheritance hierarchies by linking prototypes between constructors.

## 3. Provide an example of creating objects using the constructor/prototype pattern.

```javascript
function Person(name, age) {
  this.name = name;  // instance property
  this.age = age;
}

// Shared method on prototype
Person.prototype.greet = function() {
  console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
};

const alice = new Person("Alice", 30);
const bob = new Person("Bob", 25);

alice.greet(); // Hello, my name is Alice and I'm 30 years old.
bob.greet();   // Hello, my name is Bob and I'm 25 years old.
```
## 4. What is the purpose of the prototype property in constructor functions?

- The `prototype` property of a constructor function is used to define methods and properties that should be **shared by all instances** created using that constructor.
- It allows instances to inherit shared behavior via the prototype chain, promoting code reuse and efficient memory usage.

## 5. How do you add shared methods using the prototype of a constructor function?

- You add methods to the constructor’s prototype object by assigning functions to it.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hi, I'm ${this.name}`);
};
```
- All instances of `Person` will inherit the `greet` method without each having its own copy.
## 6. What are the advantages of using the constructor/prototype pattern over defining methods inside the constructor?

- **Memory Efficiency:** Methods on the prototype are shared by all instances, preventing duplicate copies for each instance.
- **Consistency:** Updating a prototype method affects all instances immediately.
- **Performance:** Reduced memory usage and faster method lookup due to shared methods.
- **Inheritance:** Simplifies implementing inheritance through prototype chains.

_Defining methods inside the constructor creates a new method copy for every instance, which is less efficient and uses more memory._
## 7. How does the prototype chain work when accessing properties/methods of instances created using constructors?

- When you access a property or method on an instance, JavaScript first looks for it **directly on the instance**.
- If it doesn’t find it there, it looks up the **prototype chain** by checking the instance's constructor’s prototype object.
- This continues up the chain until the property is found or the end of the chain (`null`) is reached.
- This mechanism allows instances to share methods defined on the constructor’s prototype without duplicating them.

## 8. How can you check if a property is inherited via the prototype chain or exists directly on the instance?

- Use the `hasOwnProperty()` method to check if the property exists **directly on the instance** (own property).
- If `hasOwnProperty()` returns `false`, the property is inherited via the prototype chain.

```javascript
const obj = new Person("Alice");
console.log(obj.hasOwnProperty('name')); // true (own property)
console.log(obj.hasOwnProperty('greet')); // false (inherited method from prototype)
```
## 9. Can you override prototype methods on specific instances? How?

- Yes, you can override prototype methods by defining a method with the **same name directly on the instance**.
- This instance method will **shadow** the prototype method for that specific object, while other instances still use the prototype method.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hello, I'm ${this.name}`);
};

const alice = new Person("Alice");
const bob = new Person("Bob");

// Override greet on alice instance only
alice.greet = function() {
  console.log(`Hi, this is a custom greeting from ${this.name}`);
};

alice.greet(); // Hi, this is a custom greeting from Alice
bob.greet();   // Hello, I'm Bob
```
## 10. What is the role of `instanceof` in prototype-based inheritance?

- The `instanceof` operator checks whether an object is an instance of a constructor by testing if the constructor’s prototype exists anywhere in the object’s prototype chain.
- It is used to determine if an object inherits from a particular constructor, helping identify its type or class.

```javascript
console.log(alice instanceof Person); // true
console.log(bob instanceof Person);   // true
console.log({} instanceof Person);    // false
```