## 1. How do you define a method directly on an object instance?

You define a method directly on an object instance by assigning a function to a property of that object.

```javascript
const obj = {};

obj.sayHello = function() {
  console.log("Hello!");
};

obj.sayHello(); // Hello!
```
## 2. How does defining a method directly on an object differ from defining it on the prototype?

- **Defining on the object instance:**  
  - The method is specific to that particular object only.  
  - Each instance has its own separate copy of the method, which can lead to higher memory usage if many instances are created.

- **Defining on the prototype:**  
  - The method is shared by all instances created from the constructor.  
  - Only one copy of the method exists in memory, improving efficiency.  
  - All instances inherit the method via the prototype chain unless overridden.
## 3. Will an object-specific method override the same method in its prototype?

Yes, if an object has a method defined directly on it with the same name as a method on its prototype, the object’s own method **overrides** the prototype method when accessed.

```javascript
const proto = {
  greet() {
    console.log("Hello from prototype");
  }
};

const obj = Object.create(proto);

obj.greet = function() {
  console.log("Hello from object");
};

obj.greet(); // Output: "Hello from object" — overrides prototype method
```
- The property lookup finds the method on the object first, so the prototype's method is shadowed.
## 4. What are some use cases for defining a method directly on an object rather than on the prototype?

- When you want a **unique behavior** for a specific object instance that differs from all other instances.
- To **override a prototype method** only for one particular object without affecting others.
- When dealing with **singleton objects** or objects that are not created via constructors.
- For quick, one-off methods that do not need to be shared or reused.

## 5. Provide an example of method definition on an individual object.

```javascript
const user = {
  name: "Alice",
  greet() {
    console.log(`Hello, ${this.name}!`);
  }
};

// Define a unique method only for this object
user.sayGoodbye = function() {
  console.log(`Goodbye, ${this.name}!`);
};

user.greet();       // Output: Hello, Alice!
user.sayGoodbye();  // Output: Goodbye, Alice!
```
