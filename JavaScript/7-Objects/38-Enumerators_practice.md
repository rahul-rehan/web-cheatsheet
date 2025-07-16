## 1. Which JavaScript constructs are affected by a property's enumerability?

The following JavaScript constructs only interact with **enumerable** properties:

- `for...in` loop
- `Object.keys()`
- `Object.entries()`
- `JSON.stringify()`
- `Object.assign()`

These constructs **ignore non-enumerable properties**, meaning those properties won't be included in iteration, serialization, or cloning unless explicitly accessed.

## 2. How does `for...in` interact with enumerable properties?

The `for...in` loop iterates over all **enumerable properties**, including:

- **Own properties** (defined directly on the object)
- **Inherited enumerable properties** (from the prototype chain)

It does **not** iterate over non-enumerable properties.

#### Example:
```javascript
const obj = { a: 1 };
Object.defineProperty(obj, "b", {
  value: 2,
  enumerable: false
});

for (let key in obj) {
  console.log(key); // Only "a" is logged, "b" is skipped
}
```
## 3. Do `Object.keys()` and `Object.entries()` return only enumerable properties?

**Yes**, both `Object.keys()` and `Object.entries()` return **only the object's own enumerable properties**.

- `Object.keys(obj)` returns an array of enumerable property names (keys).
- `Object.entries(obj)` returns an array of `[key, value]` pairs for enumerable properties.

They **do not include**:

- Non-enumerable properties
- Inherited properties from the prototype chain

#### Example:
```javascript
const obj = {};

Object.defineProperty(obj, "hidden", {
  value: "secret",
  enumerable: false
});

obj.visible = "shown";

console.log(Object.keys(obj));     // Output: ["visible"]
console.log(Object.entries(obj));  // Output: [["visible", "shown"]]
```
In this example, the non-enumerable property `"hidden"` is not included in the output of either method.
## 4. Does `JSON.stringify()` serialize only enumerable properties?

**Yes**, `JSON.stringify()` serializes only **own enumerable properties** of an object.

- It ignores **non-enumerable** properties.
- It also skips properties with values that are `undefined`, functions, or symbols.

#### Example:
```javascript
const obj = {
  visible: "yes"
};

Object.defineProperty(obj, "hidden", {
  value: "no",
  enumerable: false
});

console.log(JSON.stringify(obj)); // Output: {"visible":"yes"}
```
In this example, the `hidden` property is not serialized because it is not enumerable.
## 5. What is the difference between `Object.getOwnPropertyNames()` and `Object.keys()` in terms of enumerability?

- **`Object.keys(obj)`** returns an array of the object's **own enumerable property names**.
- **`Object.getOwnPropertyNames(obj)`** returns an array of **all own property names**, **regardless of whether they are enumerable or not**.

#### Example:
```javascript
const obj = {
  visible: "yes"
};

Object.defineProperty(obj, "hidden", {
  value: "no",
  enumerable: false
});

console.log(Object.keys(obj));                // Output: ["visible"]
console.log(Object.getOwnPropertyNames(obj)); // Output: ["visible", "hidden"]
```
| Method                          | Returns                        | Includes Non-Enumerable Properties |
|---------------------------------|--------------------------------|------------------------------------|
| `Object.keys(obj)`              | Own **enumerable** properties  | ❌ No                              |
| `Object.getOwnPropertyNames(obj)` | All **own** properties         | ✅ Yes                             |
