## 1. How can you get the prototype of an object in JavaScript?

You can get the prototype of an object using the built-in method:

```javascript
const prototype = Object.getPrototypeOf(obj);
```
## 2. What is the difference between `Object.getPrototypeOf()` and the `__proto__` property?

- `Object.getPrototypeOf(obj)` is the **standard and recommended** way to retrieve an object's prototype.
- `__proto__` is a **non-standard but widely supported** accessor property that exposes the internal prototype.
- `__proto__` can be read and assigned to directly, but its use is generally discouraged in favor of standard methods.
- Both usually return the same prototype object:

```javascript
const proto1 = Object.getPrototypeOf(obj);
const proto2 = obj.__proto__;

console.log(proto1 === proto2); // true
```
## 3. How can you set the prototype of an object?

You can set the prototype of an object in several ways:

1. **Using `Object.setPrototypeOf()` (standard method):**

```javascript
Object.setPrototypeOf(obj, newProto);
```
2. **Using the `__proto__` property (not recommended):**

```javascript
obj.__proto__ = newProto;
```
3. **Creating a new object with a specified prototype using `Object.create()`:**

```javascript\
const newObj = Object.create(newProto);
```
Note: Changing the prototype of an existing object using `Object.setPrototypeOf` or `__proto__` can negatively impact performance and is generally discouraged.
## 4. What does `Object.create()` do in terms of prototype linkage?

- `Object.create(proto)` creates a new object whose **prototype is set to `proto`**.  
- This means the new object inherits properties and methods from `proto` via the prototype chain.  
- It allows you to create objects with a specific prototype without calling a constructor function.

```javascript
const proto = { greet() { console.log("Hello!"); } };
const obj = Object.create(proto);

obj.greet(); // Hello!
console.log(Object.getPrototypeOf(obj) === proto); // true
```
## 5. Can you access or modify the prototype of a function constructor?

- Yes, every function in JavaScript has a `prototype` property that is used when creating instances with the `new` keyword.
- You can access and modify this `prototype` to add or change methods and properties that all instances will inherit.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log(`Hi, I'm ${this.name}`);
};

const alice = new Person("Alice");
alice.greet(); // Hi, I'm Alice

// Modify the prototype by adding a new method
Person.prototype.sayBye = function() {
  console.log("Goodbye!");
};

alice.sayBye(); // Goodbye!
```