## 1. How do you get all own enumerable string-keyed properties of an object?

You can use `Object.keys()` to retrieve an array of all **own enumerable string-keyed properties** of an object.

```javascript
const obj = { a: 1, b: 2 };
console.log(Object.keys(obj)); // ["a", "b"]
```
## 2. How do you retrieve all own property names, including non-enumerable ones?

You can use `Object.getOwnPropertyNames()` to get an array of **all own property names** (string-keyed), **including non-enumerable** properties.

#### Example:
```javascript
const obj = {};
Object.defineProperty(obj, "hidden", {
  value: 42,
  enumerable: false
});
console.log(Object.getOwnPropertyNames(obj)); // ["hidden"]
```
## 3. What does `Object.getOwnPropertyNames()` return?

`Object.getOwnPropertyNames()` returns an array of **all own string-keyed property names** of an object, **including both enumerable and non-enumerable properties**.  

It does **not** include symbol-keyed properties.

#### Example:
```javascript
const sym = Symbol("id");
const obj = { a: 1 };
obj[sym] = 2;

console.log(Object.getOwnPropertyNames(obj)); // ["a"]
console.log(Object.getOwnPropertySymbols(obj)); // [Symbol(id)]
```
## 4. What does `Object.getOwnPropertySymbols()` return?

`Object.getOwnPropertySymbols()` returns an array of **all own symbol-keyed properties** of an object.  
These properties are **not included** in `Object.getOwnPropertyNames()` or `Object.keys()`.

#### Example:
```javascript
const sym1 = Symbol("id");
const sym2 = Symbol("role");

const obj = {
  [sym1]: 123,
  [sym2]: "admin",
  name: "Alice"
};

console.log(Object.getOwnPropertySymbols(obj)); 
// Output: [Symbol(id), Symbol(role)]
```
## 5. How can you retrieve both string and symbol own property keys?

You can combine `Object.getOwnPropertyNames()` and `Object.getOwnPropertySymbols()` to get **all own property keys**, including both string and symbol keys.

#### Example:
```javascript
const obj = {
  a: 1,
  [Symbol("id")]: 123
};

const allKeys = [
  ...Object.getOwnPropertyNames(obj),
  ...Object.getOwnPropertySymbols(obj)
];

console.log(allKeys); 
// Output: ["a", Symbol(id)]
```
## 6. What is `Object.keys()` and how does it relate to own properties?

`Object.keys()` is a method that returns an array of **an object's own enumerable string-keyed property names**.  
It includes only **own properties** (not inherited) that are **enumerable** and **string-keyed**.

#### Example:
```javascript
const obj = { a: 1, b: 2 };
Object.defineProperty(obj, "hidden", {
  value: 3,
  enumerable: false
});

console.log(Object.keys(obj)); // ["a", "b"]
```
### How does `Reflect.ownKeys()` differ from `Object.keys()`?

- `Reflect.ownKeys()` returns **all own property keys** of an object, including:
  - Enumerable and non-enumerable properties
  - Both string-keyed and symbol-keyed properties

- `Object.keys()` returns only **own enumerable string-keyed** properties.

#### Example:
```javascript
const sym = Symbol("id");
const obj = {
  a: 1,
  [sym]: 2
};

Object.defineProperty(obj, "hidden", {
  value: 3,
  enumerable: false
});

console.log(Object.keys(obj)); 
// Output: ["a"]

console.log(Reflect.ownKeys(obj)); 
// Output: ["a", "hidden", Symbol(id)]
```

## Usecases and applications

## 1. Why is it useful to distinguish between own and inherited properties?

Distinguishing between **own** and **inherited** properties is important because:

- Own properties belong directly to the object, while inherited properties come from its prototype chain.
- Accessing or modifying inherited properties can lead to unexpected behavior or side effects.
- When iterating over object properties, you often want to work only with the object's own data, not properties inherited from prototypes.
- It helps avoid bugs and ensures more predictable and controlled code behavior.


## 2. Provide an example where checking for own properties prevents unintended behavior.

```javascript
const proto = { inheritedProp: 'I am inherited' };
const obj = Object.create(proto);
obj.ownProp = 'I am own';

for (const key in obj) {
  console.log(key);
}
// Output:
// ownProp
// inheritedProp

// Unintended: inheritedProp is included in iteration

// Using hasOwnProperty to filter own properties:
for (const key in obj) {
  if (obj.hasOwnProperty(key)) {
    console.log(key);
  }
}
// Output:
// ownProp
```
Without the `hasOwnProperty` check, inherited properties like `inheritedProp` can be mistakenly processed, potentially causing bugs.
## 3. How can `hasOwnProperty()` help in safely iterating over object properties?

- When using a `for...in` loop, `hasOwnProperty()` helps **filter out inherited properties**, ensuring only own properties are processed.
- This prevents unintended side effects from acting on properties inherited from the prototype chain.
- Using `hasOwnProperty()` makes your code more reliable by restricting operations to the object's own data.

#### Example:
```javascript
for (const key in obj) {
  if (obj.hasOwnProperty(key)) {
    // Safely access own property
    console.log(key, obj[key]);
  }
}
```
## 4. What precautions should be taken when `hasOwnProperty` is shadowed or missing?

- Some objects may **override** or **shadow** the `hasOwnProperty` method, or not inherit from `Object.prototype` at all, causing errors when calling `obj.hasOwnProperty()`.
- Calling `obj.hasOwnProperty()` directly in such cases can result in a **TypeError** or unexpected behavior.
- To avoid this, do **not** assume `hasOwnProperty` is always available as a method on the object.

## 5. How can you safely use `hasOwnProperty()` if an object doesn’t inherit from `Object.prototype`?

- Use `Object.prototype.hasOwnProperty.call(obj, prop)` to safely invoke `hasOwnProperty` regardless of the object's prototype.
- This ensures the method is called from `Object.prototype` directly, avoiding issues caused by shadowing or missing methods.

#### Example:
```javascript
const obj = Object.create(null); // Object with no prototype
obj.prop = 42;

// Unsafe (will throw error):
// obj.hasOwnProperty('prop'); 

// Safe:
const hasOwn = Object.prototype.hasOwnProperty.call(obj, 'prop');
console.log(hasOwn); // true
```