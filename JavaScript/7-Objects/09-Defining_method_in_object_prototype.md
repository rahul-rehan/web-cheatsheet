## 1. How do you add a method to a constructor function’s prototype?

You can add a method to the prototype by assigning a function to `ConstructorName.prototype.methodName`.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hello, my name is ${this.name}`);
};
```
## 2. What is the benefit of adding methods to the prototype instead of inside the constructor?

- Methods on the prototype are **shared by all instances**, meaning the method is created once and reused.
- Methods defined inside the constructor are **created separately for each instance**, which uses more memory.
- Using the prototype improves **memory efficiency** and allows instances to share behavior.


## 3. How does defining methods in the prototype affect memory usage across instances?

- Because all instances reference the same prototype object, **only one copy** of each method exists in memory.
- This reduces overall memory consumption compared to defining methods inside the constructor function, which creates a new copy for every instance.
## 4. Provide an example of defining a prototype method and accessing it from multiple instances.

```javascript
function Person(name) {
  this.name = name;
}

// Define method on prototype
Person.prototype.greet = function() {
  console.log(`Hello, my name is ${this.name}`);
};

const alice = new Person("Alice");
const bob = new Person("Bob");

alice.greet(); // Hello, my name is Alice
bob.greet();   // Hello, my name is Bob
```
Both `alice` and `bob` share the same `greet` method defined on `Person.prototype`.
## 5. Can you overwrite a prototype method for a specific instance?

Yes, you can overwrite a prototype method for a specific instance by assigning a new function directly to that instance’s method name. This will shadow the prototype method for that instance only.

```javascript
const alice = new Person("Alice");

// Overwrite greet method only for alice instance
alice.greet = function() {
  console.log(`Hi, I'm ${this.name} (custom greeting)`);
};

alice.greet(); // Hi, I'm Alice (custom greeting)
const bob = new Person("Bob");
bob.greet();   // Hello, my name is Bob (original prototype method)
```
- The `greet` method on `alice` now overrides the one on the prototype.

- Other instances like `bob` still use the prototype method.