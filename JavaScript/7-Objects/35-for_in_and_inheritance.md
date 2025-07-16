## 1. Does `for...in` iterate over inherited properties?

Yes, the `for...in` loop **does iterate over inherited enumerable properties** from the object's prototype chain, in addition to the object's own properties.

## 2. How can you prevent a `for...in` loop from accessing inherited properties?

To avoid iterating over inherited properties in a `for...in` loop, you can use the `Object.prototype.hasOwnProperty()` method to check if a property belongs **directly to the object**.

**Example:**
```javascript
const obj = {
  a: 1,
  b: 2
};

Object.prototype.c = 3; // Inherited property

for (let key in obj) {
  if (obj.hasOwnProperty(key)) {
    console.log(key); // Only logs "a" and "b"
  }
}
```
## 3. What is `Object.prototype.hasOwnProperty()` and how is it used with `for...in`?

`Object.prototype.hasOwnProperty()` is a method that checks whether a property is a **direct (own) property** of an object, as opposed to one inherited from the prototype chain.

It returns `true` if the property exists directly on the object and `false` if it is inherited.

#### ✅ Usage with `for...in`:

When using a `for...in` loop, it's recommended to use `hasOwnProperty()` to filter out inherited properties:

```javascript
const obj = {
  name: "Alice",
  age: 25
};

Object.prototype.role = "admin"; // Inherited property

for (let key in obj) {
  if (obj.hasOwnProperty(key)) {
    console.log(`${key}: ${obj[key]}`);
  }
}
```
### Output:

```makefile
name: Alice
age: 25
```
This ensures that only the object's own properties are processed.
## 4. Provide an example where `for...in` includes properties from the prototype chain

```javascript
const parent = {
  inheritedProp: "I am inherited"
};

const child = Object.create(parent);
child.ownProp = "I am own property";

for (let key in child) {
  console.log(`${key}: ${child[key]}`);
}
```
#### Output:

```vbnet
ownProp: I am own property
inheritedProp: I am inherited
```
In this example, `for...in` iterates over both the own property (`ownProp`) and the inherited property (`inheritedProp`).
## 5. Why is it important to check for own properties in `for...in` loops?

It is important to check for **own properties** when using `for...in` because:

- The `for...in` loop iterates over **all enumerable properties**, including those inherited through the **prototype chain**.
- Processing inherited properties can lead to **unexpected behavior**, especially if prototypes have been extended or modified.
- It helps prevent **bugs** and ensures your logic only applies to properties that **belong directly to the object**.

#### Example:
```javascript
const obj = {
  a: 1,
  b: 2
};

Object.prototype.c = 3; // Inherited property

for (let key in obj) {
  if (obj.hasOwnProperty(key)) {
    console.log(`${key}: ${obj[key]}`);
  }
}
```
#### Output:

```makefile
a: 1
b: 2
```
This ensures inherited properties like `c` are excluded from the loop logic.