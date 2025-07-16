## 1. How do you add a method inside a constructor function so that each instance gets a copy?

- To give each instance its own copy of a method, define the method **inside** the constructor using `this`.

#### Example:

```javascript
function Person(name) {
  this.name = name;
  this.sayHello = function() {
    console.log(`Hello, my name is ${this.name}`);
  };
}

const p1 = new Person("Alice");
const p2 = new Person("Bob");

p1.sayHello === p2.sayHello; // false — each has its own copy
```
## 2. How do you add a method to the constructor function’s prototype?

- To ensure all instances share the same method (saving memory), add the method to the constructor’s `prototype` property.
- This makes the method available to all instances created with `new`, without duplicating it for each one.

#### Example:

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function() {
  console.log(`Hello, my name is ${this.name}`);
};

const p1 = new Person("Alice");
const p2 = new Person("Bob");

p1.sayHello(); // Output: Hello, my name is Alice
p2.sayHello(); // Output: Hello, my name is Bob

console.log(p1.sayHello === p2.sayHello); // true — shared method
```
Defining methods on the prototype is more memory-efficient and preferred for shared behavior.
## 3. What are the pros and cons of defining methods inside the constructor vs on the prototype?

| Method Location           | Pros                                                      | Cons                                               |
|--------------------------|-----------------------------------------------------------|----------------------------------------------------|
| **Inside the constructor** | - Each instance gets its own copy of the method.<br>- Methods can access instance-specific data easily.<br>- Useful if methods need to be unique per instance. | - Higher memory usage since every instance has its own method copy.<br>- Slower creation of instances. |
| **On the prototype**       | - Methods are shared among all instances, saving memory.<br>- Faster instance creation.<br>- Keeps behavior consistent across instances. | - Cannot have per-instance variations of the method easily.<br>- `this` context depends on how the method is called. |

> **Summary:**  
> Use **prototype methods** for shared behavior to optimize memory and performance.  
> Define methods **inside constructors** only if you need instance-specific methods or closures.
## 4. Provide an example of adding a shared method using `ConstructorName.prototype.methodName`

You can add methods that are shared across all instances by attaching them to the constructor’s prototype:

```javascript
function Person(name) {
  this.name = name;
}

// Adding a shared method to the prototype
Person.prototype.sayHello = function() {
  console.log(`Hello, my name is ${this.name}`);
};

const alice = new Person("Alice");
const bob = new Person("Bob");

alice.sayHello(); // Output: Hello, my name is Alice
bob.sayHello();   // Output: Hello, my name is Bob
```
## 5. Can you add methods to an instance after it has been created? How?

- Yes, you can add methods directly to a specific instance by assigning a function to a property on that instance.

#### Example:

```javascript
const person = new Person("Charlie");

// Add a method only to this instance
person.sayGoodbye = function() {
  console.log(`Goodbye from ${this.name}`);
};

person.sayGoodbye(); // Output: Goodbye from Charlie

// This method is not available on other instances
const anotherPerson = new Person("Dave");
anotherPerson.sayGoodbye(); // Error: sayGoodbye is not a function
```
Methods added this way are unique to the instance and do not affect other instances or the prototype.