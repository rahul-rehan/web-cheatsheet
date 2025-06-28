# Prototypes in JavaScript

## 1. What is a prototype in JavaScript?

In JavaScript, **a prototype is an object from which other objects inherit properties and methods**. Every JavaScript object has an internal link to another object called its prototype. This forms a prototype chain, enabling inheritance and sharing behavior between objects.

---

## 2. How is the [[Prototype]] of an object accessed in modern JavaScript?

The internal `[[Prototype]]` of an object can be accessed using:

- `Object.getPrototypeOf(obj)` — to get the prototype of `obj`.
- `Object.setPrototypeOf(obj, proto)` — to set the prototype of `obj`.

Modern JavaScript discourages using the deprecated `__proto__` property directly.

---

## 3. What is the difference between __proto__ and prototype?

- `__proto__` is a **property of an object instance** that points to its prototype (the actual object it inherits from).
- `prototype` is a **property of constructor functions** (like `function Person() {}`) that is used to set the `[[Prototype]]` of all objects created by that constructor via `new`.

In short:

- `obj.__proto__` → the prototype of the object instance.
- `Func.prototype` → the prototype object that will become the prototype of instances created by `new Func()`.

---

## 4. What is the default prototype of an object created with an object literal?

An object created with an object literal `{}` has its `[[Prototype]]` set to `Object.prototype` by default. This means it inherits standard methods like `toString()`, `hasOwnProperty()`, etc., from `Object.prototype`.
## 5. How does JavaScript implement inheritance using prototypes?

JavaScript uses **prototypal inheritance**, where objects inherit directly from other objects. Every object has an internal link (called `[[Prototype]]`) to another object (its prototype). When you try to access a property or method on an object, JavaScript looks for it on the object itself. If not found, it looks up the prototype chain, checking the prototype object, then the prototype's prototype, and so on, until it finds the property or reaches `null`.

---

## 6. What is prototypal inheritance and how is it different from classical inheritance?

- **Prototypal inheritance** is based on objects inheriting directly from other objects. There's no concept of classes; instead, inheritance happens via prototype chains.
  
- **Classical inheritance** (used in languages like Java or C++) involves classes, blueprints for creating instances, and inheritance hierarchies between classes.

JavaScript originally used prototypal inheritance but from ES6 onwards, `class` syntax was introduced as syntactic sugar on top of prototypal inheritance. This means that even `class`-based inheritance works through prototypes behind the scenes.

---

## 7. What is the prototype chain in JavaScript?

The **prototype chain** is the series of linked prototype objects that JavaScript follows when looking up a property or method. If a property is not found on an object, the engine checks its prototype, then that prototype's prototype, continuing upward until it finds the property or reaches the end (`null`).

---

## 8. How does the prototype chain work when accessing a property or method?

When you access a property or method on an object:

1. JavaScript first looks for the property directly on the object.
2. If not found, it looks on the object's prototype.
3. If still not found, it looks on the prototype's prototype.
4. This process continues up the prototype chain until the property is found or the chain ends.
5. If the property is not found anywhere, `undefined` is returned.

Example:

```javascript
const parent = { greet() { console.log("Hello"); } };
const child = Object.create(parent);

child.greet(); // "Hello" - found via prototype chain

console.log(child.hasOwnProperty('greet')); // false - greet is not own property
```
## 9. What happens if a property is not found in an object or its prototype chain?

If JavaScript cannot find a property on the object itself **or anywhere up its prototype chain**, the result of accessing that property is **`undefined`**. No error is thrown; it simply returns `undefined`.

---

## 10. What is the role of `Object.prototype` in JavaScript?

`Object.prototype` is the **top-level prototype object** from which almost all JavaScript objects inherit. It provides a base set of properties and methods (like `toString()`, `hasOwnProperty()`, etc.). The prototype chain ultimately ends here because `Object.prototype`'s own prototype is `null`.

---

## 11. What are some built-in methods available on `Object.prototype`?

Common methods available on `Object.prototype` include:

- `toString()`
- `hasOwnProperty(prop)`
- `isPrototypeOf(obj)`
- `valueOf()`
- `propertyIsEnumerable(prop)`
- `toLocaleString()`

These methods are inherited by all objects unless overridden.

---

## 12. How do you create an object with no prototype? Why would you do that?

You can create an object with **no prototype** by using:

```javascript
const obj = Object.create(null);
```
Such an object:

- Does **not** inherit from `Object.prototype`.
- Has no built-in methods like `toString()` or `hasOwnProperty()`.

Why do this?

- To create a "plain" object with no inherited properties, useful when you want a pure dictionary/map without prototype pollution.
- It avoids potential issues where inherited properties interfere with keys, especially when using the object as a map.
## 13. How can you manually set the prototype of an object?

You can manually set the prototype of an object using:

- `Object.setPrototypeOf(obj, prototype)` — sets the prototype of `obj` to `prototype`.
- Using the `__proto__` property (not recommended for performance reasons and deprecated in some contexts).

Example:

```javascript
const proto = { greet() { console.log('Hello'); } };
const obj = {};
Object.setPrototypeOf(obj, proto);
obj.greet();  // Outputs: Hello
```
## 14. What is the purpose of Object.create()? Provide an example.

`Object.create()` creates a new object with the specified prototype object and optional properties.

Example:

```javascript
const proto = {
  greet() { console.log('Hi!'); }
};

const obj = Object.create(proto);
obj.greet();  // Outputs: Hi!
```
This is useful for creating objects that inherit directly from a given prototype without needing constructor functions.
## 15. What does the constructor property refer to?

The `constructor` property refers to the function that created the instance's prototype.

For example:

```javascript
function Person(name) {
  this.name = name;
}
const p = new Person('Alice');

console.log(p.constructor === Person);  // true
```
The `constructor` property is typically found on the prototype object and links back to the constructor function.
## 16. How do function constructors and their `.prototype` property work?

A function constructor is a regular function used with the `new` keyword to create object instances.

Each function has a `.prototype` property, which is an object used as the prototype for all instances created by that constructor.

Properties and methods defined on the `.prototype` object are shared by all instances.

Example:

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  console.log('Hello, ' + this.name);
};

const alice = new Person('Alice');
alice.greet();  // Outputs: Hello, Alice
```
Here, `greet` is defined once on `Person.prototype` and accessible by all instances.
## 17. How can you add a method to all instances of a constructor function?

You add methods to the constructor function’s `.prototype` object. All instances created using that constructor will then share these methods.

Example:
```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function() {
  console.log(`Hello, my name is ${this.name}`);
};

const alice = new Person('Alice');
alice.sayHello();  // Hello, my name is Alice
```
## 18. What is the difference between instance properties and prototype properties?

- **Instance properties** are defined directly on each object instance (usually inside the constructor using `this`). They are unique to each instance.

- **Prototype properties** are defined on the constructor’s prototype object and shared by all instances. These include methods or properties common to all instances.
## 19. How do ES6 class and extends relate to prototypal inheritance internally?

ES6 class syntax is syntactic sugar over the prototypal inheritance model.

When you use `class` and `extends`, JavaScript internally sets up the prototype chain so the subclass’s prototype object inherits from the superclass’s prototype.

Methods defined inside classes go on the prototype of the class, making them shared among instances.

**Example:**

```javascript
class Animal {
  speak() {
    console.log('Animal speaks');
  }
}

class Dog extends Animal {
  speak() {
    console.log('Dog barks');
  }
}

const dog = new Dog();
dog.speak();  // Dog barks
```
## 20. Can you modify the prototype of an existing object? What are the implications?

Yes, you can modify an object's prototype using `Object.setPrototypeOf(obj, newProto)` or by assigning to `__proto__` (not recommended).

**Implications:**

- Changing the prototype at runtime is slow and can negatively impact performance.
- It can break assumptions about the object's structure and cause bugs.
- It’s generally better to set the prototype when the object is created (e.g., using `Object.create`).
## 21. What is the result of `obj.hasOwnProperty(prop)`? How is it useful?

- **Result:**  
  Returns `true` if the object `obj` has the property `prop` as its **own (direct)** property, not inherited through the prototype chain. Otherwise, it returns `false`.

- **Usefulness:**  
  It helps distinguish between properties that belong directly to the object and those inherited from its prototype. This is useful to avoid accidentally accessing or modifying inherited properties.

---

## 22. What are the downsides of modifying `Object.prototype`?

- Modifying `Object.prototype` affects **all objects** because every object inherits from it.  
- It can lead to **unexpected behavior and bugs**, especially if property names collide with user-defined properties.  
- It can **break for-in loops** and other iterations if properties are added that are enumerable by default.  
- Generally considered **bad practice** as it pollutes the global object space and makes code harder to maintain and debug.

---

## 23. How can you determine if an object inherits from another object?

- You can use the **`instanceof`** operator:  
  ```js
  obj instanceof ConstructorFunction
  ```
  Returns `true` if `ConstructorFunction.prototype` exists anywhere in `obj’s` prototype chain.
- You can also use `Object.getPrototypeOf()` or `__proto__` to traverse the prototype chain manually.
- The `isPrototypeOf()` method checks if an object exists in another object's prototype chain:
    ```js
    prototypeObj.isPrototypeOf(obj)
    ```
## 24. What is `Object.getPrototypeOf()` and how is it used?

`Object.getPrototypeOf()` is a built-in JavaScript method that returns the prototype (i.e., the internal `[[Prototype]]`) of the specified object.

#### Usage:

```js
const prototype = Object.getPrototypeOf(obj);
```
- It retrieves the object from which `obj` inherits properties and methods.

- Useful for inspecting or working with an object's prototype chain.

- Helps understand inheritance relationships between objects.

**Example:**

```js
const obj = {};
const proto = Object.getPrototypeOf(obj);

console.log(proto === Object.prototype);  // true
```
In this example, `obj` is an empty object literal whose prototype is `Object.prototype`.
## 25. What is the output of the following code?

```javascript
function A() {}
A.prototype.greet = function() {
  return "Hi";
};
const a = new A();
console.log(a.greet());
```
The output of the code is:
```js
Hi
```

**Explanation:**

- A function constructor `A` is defined.
- A method `greet` is added to `A.prototype`.
- An instance `a` of `A` is created using `new A()`.
- When `a.greet()` is called, JavaScript looks for `greet` on the instance `a`. Since it’s not found directly on `a`, it looks up the prototype chain and finds `greet` on `A.prototype`.
- The method returns `"Hi"`, which is then logged.
