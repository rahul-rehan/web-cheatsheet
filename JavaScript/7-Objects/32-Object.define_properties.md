## 1. What is `Object.defineProperties()` in JavaScript?

`Object.defineProperties()` is a method in JavaScript used to define or modify multiple properties on an object at once. Each property can be configured with descriptors such as `value`, `writable`, `enumerable`, `configurable`, `get`, and `set`.

## 2. How Does `Object.defineProperties()` Differ from `Object.defineProperty()`?

- `Object.defineProperty()` defines or modifies a **single** property on an object.
- `Object.defineProperties()` defines or modifies **multiple** properties at once.

Both allow precise control over property behavior using descriptors.

## 3. Example: Defining Multiple Properties Using `Object.defineProperties()`

```javascript
const person = {};

Object.defineProperties(person, {
  firstName: {
    value: 'Jane',
    writable: true,
    enumerable: true,
    configurable: true
  },
  lastName: {
    value: 'Doe',
    writable: true,
    enumerable: true,
    configurable: true
  },
  fullName: {
    get() {
      return `${this.firstName} ${this.lastName}`;
    },
    enumerable: true,
    configurable: true
  }
});

console.log(person.fullName); // "Jane Doe"
```
This approach is useful when initializing objects with several well-defined properties.
## 4. Can You Use `Object.defineProperties()` to Mix Data and Accessor Properties? How?

Yes, `Object.defineProperties()` allows you to define both **data properties** and **accessor properties** (getters/setters) on the same object in a single call.

Example:

```javascript
const book = {};

Object.defineProperties(book, {
  title: {
    value: 'JavaScript Essentials',
    writable: true,
    enumerable: true,
    configurable: true
  },
  author: {
    value: 'Jane Doe',
    writable: true,
    enumerable: true,
    configurable: true
  },
  info: {
    get() {
      return `${this.title} by ${this.author}`;
    },
    enumerable: true,
    configurable: true
  }
});

console.log(book.info); // "JavaScript Essentials by Jane Doe"
```
In this example, `title` and `author` are data properties, while `info` is an accessor property.
## 5. What is the Return Value of `Object.defineProperties()`?

The `Object.defineProperties()` method returns the **same object** that is passed as the first argument. It does **not** create a new object.

#### Example:

```javascript
const obj = {};
const result = Object.defineProperties(obj, {
  a: { value: 1, writable: true }
});

console.log(result === obj); // true
```
This behavior allows for chaining or immediate usage of the modified object after defining multiple properties.