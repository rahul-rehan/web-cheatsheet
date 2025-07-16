## 1. How do you make a property non-enumerable using `Object.defineProperty()`?

You can make a property non-enumerable by setting the `enumerable` attribute to `false` when using `Object.defineProperty()`.

#### Syntax:
```javascript
Object.defineProperty(obj, "propertyName", {
  value: "value",
  enumerable: false
});
```
## 2. Example: Defining a non-enumerable property and verifying its visibility in a `for...in` loop

```javascript
const user = {
  name: "Alice"
};

// Define a non-enumerable property
Object.defineProperty(user, "age", {
  value: 30,
  enumerable: false
});

// Iterate using for...in
for (let key in user) {
  console.log(key); // Output: "name" (but not "age")
}

console.log(user.age); // Output: 30 (accessible directly)
```
#### In this example:

- The property `age` is defined as non-enumerable using `Object.defineProperty()`.

- It does not appear in the `for...in` loop.

- However, it is still accessible directly on the object.
## 3. Can accessor properties (getters/setters) be enumerable?

Yes, accessor properties defined with getters and/or setters **can be enumerable**.

By default, when you define an accessor property using `Object.defineProperty()`, the `enumerable` attribute is set to `false`. You need to explicitly set `enumerable: true` to make them enumerable.

#### Example:
```javascript
const obj = {};

Object.defineProperty(obj, "greeting", {
  get() {
    return "Hello!";
  },
  enumerable: true
});

for (let key in obj) {
  console.log(key); // Outputs: "greeting"
}
```
In this example, the accessor property `greeting` is enumerable and will appear in a `for...in` loop.
## 4. Can you change the enumerability of an existing property? How?

Yes, you can change the enumerability of an existing property using `Object.defineProperty()` by redefining the property descriptor and setting the `enumerable` attribute.

#### Example:
```javascript
const obj = { name: "Alice" };

// Initially enumerable (default for object literal properties)
console.log(obj.propertyIsEnumerable("name")); // true

// Change 'name' property to non-enumerable
Object.defineProperty(obj, "name", {
  enumerable: false
});

console.log(obj.propertyIsEnumerable("name")); // false
```
This updates the `enumerable` attribute without affecting the property's value or other attributes.
## 5. What happens when you use `Object.defineProperties()` with `{ enumerable: false }`?

When you use `Object.defineProperties()` and set `{ enumerable: false }` for a property, that property becomes **non-enumerable** on the object.

This means:

- The property **will not appear** in enumeration methods such as `for...in` loops or `Object.keys()`.
- The property remains **accessible directly** via the object.

#### Example:
```javascript
const obj = {};

Object.defineProperties(obj, {
  visible: {
    value: "yes",
    enumerable: true
  },
  hidden: {
    value: "no",
    enumerable: false
  }
});

console.log(Object.keys(obj)); // Output: ["visible"]

for (let key in obj) {
  console.log(key); // Output: "visible" only
}

console.log(obj.hidden); // Output: "no" (accessible directly)
```