## 1. What is a Property Descriptor in JavaScript?

A **property descriptor** is an object that describes the configuration of a property on a JavaScript object. It defines how a property behaves — such as whether it can be changed, enumerated, or configured.

There are two main types of property descriptors:
- **Data descriptors**: Describe a property with a value.
- **Accessor descriptors**: Describe a property with a getter and/or setter.


## 2. How Can You Retrieve a Property Descriptor?

You can retrieve a property descriptor using the `Object.getOwnPropertyDescriptor()` method.

#### Syntax:

```javascript
Object.getOwnPropertyDescriptor(object, propertyName);
```
#### Example:
```javascript
const person = { name: 'Alice' };
const descriptor = Object.getOwnPropertyDescriptor(person, 'name');
console.log(descriptor);
```
#### Output:

```javascript
{
  value: 'Alice',
  writable: true,
  enumerable: true,
  configurable: true
}
```
## 3. What Attributes Are Available in a Data Property Descriptor?

A **data property descriptor** in JavaScript includes the following attributes:

- **`value`**: The actual value of the property.
- **`writable`**: A boolean indicating if the property’s value can be changed.
- **`enumerable`**: A boolean indicating if the property shows up during enumeration (e.g., in `for...in` loops or `Object.keys()`).
- **`configurable`**: A boolean indicating if the property descriptor can be changed and if the property can be deleted from the object.

#### Example:

```javascript
const obj = { name: 'Alice' };
const descriptor = Object.getOwnPropertyDescriptor(obj, 'name');

console.log(descriptor);
// Output:
// {
//   value: 'Alice',
//   writable: true,
//   enumerable: true,
//   configurable: true
// }
```
## 4. What Attributes Are Available in an Accessor Property Descriptor?

An **accessor property descriptor** in JavaScript contains the following attributes:

- **`get`**: A function that serves as a getter for the property. If not specified, defaults to `undefined`.
- **`set`**: A function that serves as a setter for the property. If not specified, defaults to `undefined`.
- **`enumerable`**: A boolean indicating whether the property is enumerable.
- **`configurable`**: A boolean indicating whether the property descriptor can be changed and if the property can be deleted.

> Note: Accessor descriptors **do not** have `value` or `writable` attributes.

## 5. What Is the Default Value of `enumerable`, `writable`, and `configurable` When Using `Object.defineProperty()`?

When defining a property using `Object.defineProperty()` and **not specifying** any of the descriptor attributes, the following defaults apply:

- `writable`: `false`
- `enumerable`: `false`
- `configurable`: `false`

#### Example:

```javascript
const obj = {};
Object.defineProperty(obj, 'key', { value: 42 });

console.log(Object.getOwnPropertyDescriptor(obj, 'key'));
// Output:
// {
//   value: 42,
//   writable: false,
//   enumerable: false,
//   configurable: false
// }
```
## 6. What Happens if a Property Is Marked `configurable: false`?

If a property is defined with `configurable: false`, the following restrictions apply:

- The property **cannot be deleted** using the `delete` operator.
- The property **cannot be reconfigured** (i.e., you cannot change its descriptor attributes such as `enumerable`, `configurable`, or `writable`).
- If it is a data property, you **cannot change its `writable` attribute** from `false` to `true`.
- You **can still change the value** of the property if it is writable (`writable: true`).
- Attempting to redefine or delete the property will throw an error in strict mode.

#### Example:

```javascript
const obj = {};
Object.defineProperty(obj, 'prop', {
  value: 42,
  configurable: false,
  writable: true
});

delete obj.prop; // false (cannot delete)
obj.prop = 100;  // works because writable: true

// Attempt to redefine property will throw an error
Object.defineProperty(obj, 'prop', {
  configurable: true
}); // TypeError: Cannot redefine property: prop
```
Once `configurable` is set to `false`, the property is locked down from structural changes.
## 7. How do enumerable and configurable affect iteration and deletion?

- **enumerable**:  
  Determines whether a property shows up during property enumeration methods like `for...in` loops or `Object.keys()`.  
  - If `enumerable: false`, the property will be skipped during enumeration.  
  - If `enumerable: true`, the property will appear in enumerations.

- **configurable**:  
  Controls whether a property descriptor can be changed and whether the property can be deleted from the object.  
  - If `configurable: false`, you cannot delete the property or change its descriptor (except for `writable` from `true` to `false`).  
  - If `configurable: true`, you can delete the property or modify its descriptor.

## 8. Can you convert a data property into an accessor property after it is defined?

No, you **cannot** convert a data property into an accessor property if the property is marked as `configurable: false`. If `configurable: true`, you can redefine the property with `Object.defineProperty()` to change it from a data property to an accessor property.

Example:

```js
const obj = {};
Object.defineProperty(obj, 'prop', {
  value: 42,
  writable: true,
  enumerable: true,
  configurable: true,
});

// Convert data property to accessor property
Object.defineProperty(obj, 'prop', {
  get() { return 100; },
  set(val) { console.log('Setter called with', val); },
  enumerable: true,
  configurable: true,
});
```