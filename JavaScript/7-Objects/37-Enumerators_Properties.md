## 1. What does it mean for a property to be "enumerable" in JavaScript?

In JavaScript, a property is considered **enumerable** if it is set to show up during property enumeration processes, such as:

- `for...in` loops
- `Object.keys()`
- `JSON.stringify()`

By default, properties created using object literals or `Object.defineProperty()` (with `enumerable: true`) are enumerable.

## 2. Which internal attribute determines whether a property is enumerable?

Each property in JavaScript has an internal attribute called **`[[Enumerable]]`**. This attribute determines whether the property can be **enumerated** in loops like `for...in`.

If `[[Enumerable]]` is set to `true`, the property is enumerable. If it's `false`, the property is hidden from enumerations.

## 3. How do you check if a property is enumerable on an object?

You can check if a property is enumerable using the `propertyIsEnumerable()` method.

**Example:**
```javascript
const obj = {
  name: "Alice"
};

console.log(obj.propertyIsEnumerable("name")); // true

// Define a non-enumerable property
Object.defineProperty(obj, "age", {
  value: 30,
  enumerable: false
});

console.log(obj.propertyIsEnumerable("age")); // false
```
This method returns `true` if the property is both present on the object and enumerable.
## 4. Are properties created using object literals (`{}`) enumerable by default?

Yes, properties created using **object literals** are **enumerable by default**.

**Example:**
```javascript
const obj = {
  name: "Alice",
  age: 30
};

console.log(Object.keys(obj)); // ["name", "age"]
console.log(obj.propertyIsEnumerable("name")); // true
```
In this case, both `name` and `age` are enumerable.
## 5. Are properties created using `Object.defineProperty()` enumerable by default?

**No**, properties created using `Object.defineProperty()` are **not enumerable by default**.  
If you do not explicitly set the `enumerable` attribute to `true`, it defaults to `false`.

#### Example:
```javascript
const obj = {};

Object.defineProperty(obj, "name", {
  value: "Alice"
});

console.log(Object.keys(obj));               // Output: []
console.log(obj.propertyIsEnumerable("name")); // Output: false
```
In this example, the `"name"` property is not enumerable, so it does not show up in `Object.keys()`.

#### To make it enumerable:
```javascript
Copy
Edit
Object.defineProperty(obj, "age", {
  value: 30,
  enumerable: true
});

console.log(Object.keys(obj));               // Output: ["age"]
console.log(obj.propertyIsEnumerable("age")); // Output: true
```
By setting `enumerable: true`, the property becomes visible in enumerations like `for...in` and `Object.keys()`.