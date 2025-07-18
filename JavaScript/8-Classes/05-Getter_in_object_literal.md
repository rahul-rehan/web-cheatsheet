## 1. How do you define a getter for a computed value inside an object literal?

You define a getter using the `get` keyword followed by the property name and a function that returns the computed value.

## 2. Can a getter access other properties of the same object using `this`?

Yes, a getter can access other properties of the same object using `this` to compute and return a value dynamically.

## 3. Provide an example of a getter that returns a derived or formatted value.

```js
const person = {
  firstName: "John",
  lastName: "Doe",
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
};

console.log(person.fullName); // Output: John Doe
```
In this example, the `fullName` getter computes a formatted string combining `firstName` and `lastName`.
## 4. What happens if you try to assign a value to a property that only has a getter?

If you try to assign a value to a property that has only a getter (no setter), the assignment will fail silently in non-strict mode, or throw a `TypeError` in strict mode. The property's value cannot be changed because there is no setter to handle the assignment.

## 5. Can getters be enumerable? How can you check this?

Yes, getters can be enumerable if their property descriptor has the `enumerable` attribute set to `true`. To check if a getter property is enumerable, you can use `Object.getOwnPropertyDescriptor()` and inspect the `enumerable` property.

#### Example:

```js
const obj = {};
Object.defineProperty(obj, 'prop', {
  get() { return 42; },
  enumerable: true,
});

console.log(Object.getOwnPropertyDescriptor(obj, 'prop').enumerable); // true
```