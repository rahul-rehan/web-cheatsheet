## 1. How do you define a data property using object literal syntax?

You can define a data property simply by specifying a key-value pair inside an object literal:

```js
const obj = {
  name: 'Alice',
  age: 30
};
```
Here, `name` and `age` are data properties with the values `'Alice'` and `30`.
## 2. What are the default attributes of a data property?

When you define a data property using an object literal, its default property attributes are:

- **writable:** `true` — the property's value can be changed.
- **enumerable:** `true` — the property will show up during enumeration, such as in `for...in` loops.
- **configurable:** `true` — the property descriptor can be changed and the property can be deleted.
## 3. How can you define a data property using `Object.defineProperty()`?

You can define a data property on an object with specific attributes using `Object.defineProperty()`:

```javascript
Object.defineProperty(obj, 'propertyName', {
  value: 42,           // The value of the property
  writable: true,      // Can the property be changed?
  enumerable: true,    // Will the property show up during enumeration?
  configurable: true   // Can the property descriptor be changed and property deleted?
});
```
This method allows precise control over the property's behavior compared to object literals.
## 4. Example of Creating a Non-Writable or Non-Enumerable Property

```javascript
const obj = {};

// Non-writable property
Object.defineProperty(obj, 'constant', {
  value: 100,
  writable: false,     // Cannot be changed after definition
  enumerable: true,
  configurable: true
});

// Non-enumerable property
Object.defineProperty(obj, 'hidden', {
  value: 'secret',
  writable: true,
  enumerable: false,   // Won't appear in for...in or Object.keys()
  configurable: true
});

console.log(obj.constant); // 100
console.log(obj.hidden);   // 'secret'
console.log(Object.keys(obj)); // ['constant'] - 'hidden' is not listed
```
## 5. What Happens if You Try to Change a `writable: false` Property?

- In **strict mode**, attempting to assign a new value to a non-writable property throws a **TypeError**.
- In **non-strict mode**, the assignment fails silently without changing the property's value.

Example:

```javascript
'use strict';

const obj = {};
Object.defineProperty(obj, 'constant', {
  value: 100,
  writable: false
});

obj.constant = 200; // TypeError: Cannot assign to read only property 'constant'
```