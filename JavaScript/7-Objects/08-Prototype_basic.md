## 1. What is a prototype in JavaScript?

- A **prototype** is an object that is associated with every JavaScript function and object by default.
- It acts as a blueprint from which other objects inherit properties and methods.
- When you create a function, JavaScript automatically assigns a `prototype` property to it — this prototype object is used when creating instances with `new`.

## 2. How is the prototype chain used for inheritance in JavaScript?

- The **prototype chain** is a series of linked prototype objects used to implement inheritance.
- When accessing a property or method on an object, JavaScript:
  1. Looks for the property directly on the object.
  2. If not found, looks up the object's internal `[[Prototype]]` (accessible via `__proto__`).
  3. This process continues up the chain until the property is found or the end (`null`) is reached.
- This allows objects to inherit properties and methods from their prototypes.

## 3. What is the difference between `__proto__` and `prototype`?

| Property       | Description                                                   | Exists On          |
| -------------- | ------------------------------------------------------------- | ------------------ |
| `prototype`    | An object property of a **function** that is used as a template for instances created by that function (constructor). | Functions          |
| `__proto__`    | An internal reference (accessor property) pointing to the object's **prototype** (i.e., the object it inherits from). Used to access the prototype chain at runtime. | All objects (instances) |

- In short:
  - `prototype` is a property of constructor functions.
  - `__proto__` is the actual prototype reference of an object instance.

#### Example:

```javascript
function Person(name) {
  this.name = name;
}

console.log(Person.prototype);  // Object that will be the prototype of instances
const p = new Person("Alice");
console.log(p.__proto__ === Person.prototype);  // true
```
## 4. What is the default prototype of an object created using object literal `{}`?

- The default prototype of an object created with an object literal (`{}`) is `Object.prototype`.
- This means such objects inherit properties and methods from `Object.prototype`, like `.toString()`, `.hasOwnProperty()`, etc.

```javascript
const obj = {};
console.log(Object.getPrototypeOf(obj) === Object.prototype); // true
```
## 5. What is the prototype of a function in JavaScript?

- Every function in JavaScript has a `prototype` property.
- This `prototype` object is used as the prototype for instances created when the function is called with the `new` keyword (i.e., when the function is used as a constructor).
- Besides, functions themselves are objects and inherit from `Function.prototype`.

#### Example:

```javascript
function greet() {}

console.log(typeof greet.prototype); // "object" — the prototype object for instances
console.log(Object.getPrototypeOf(greet) === Function.prototype); // true — functions inherit from Function.prototype
```
## 6. How does JavaScript use the prototype chain during property or method lookup?

- When you access a property or method on an object, JavaScript follows this process:
  1. Checks if the property exists directly on the object itself.
  2. If not found, looks up the object's prototype (`__proto__` or internal `[[Prototype]]`).
  3. Continues searching up the prototype chain until the property is found or the chain ends (`null`).
- This allows objects to inherit properties and methods from their prototypes.

#### Example:

```javascript
const obj = {};
console.log(obj.toString()); // Found on Object.prototype
```