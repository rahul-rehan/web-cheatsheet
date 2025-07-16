## 1. Do inherited properties affect enumeration?

Yes, **inherited enumerable properties** are included in enumeration by the `for...in` loop.  
The `for...in` loop iterates over both the object's own enumerable properties **and** enumerable properties inherited through the prototype chain.

However, methods like `Object.keys()` and `Object.entries()` only return the object's **own enumerable properties**, ignoring inherited ones.

## 2. Does `hasOwnProperty()` check if a property is enumerable?

No, the method `hasOwnProperty()` **only checks if a property is an own property** of the object.  
It does **not** check whether the property is enumerable or not.

#### Example:
```javascript
const obj = {};
Object.defineProperty(obj, "hidden", {
  value: "secret",
  enumerable: false
});

console.log(obj.hasOwnProperty("hidden")); // true
console.log(obj.propertyIsEnumerable("hidden")); // false
```
## 3. Are symbol-keyed properties enumerable by default?

No, **symbol-keyed properties are not enumerable by default** in typical property enumeration methods such as `for...in` or `Object.keys()`.

- Symbol-keyed properties do **not** appear in `for...in` loops, `Object.keys()`, or `JSON.stringify()`.
- To access symbol-keyed properties, you can use `Object.getOwnPropertySymbols()`.

#### Example:
```javascript
const sym = Symbol("id");
const obj = {
  [sym]: 123,
  name: "Alice"
};

for (let key in obj) {
  console.log(key); // Outputs: "name" only
}

console.log(Object.getOwnPropertySymbols(obj)); // Output: [Symbol(id)]
```
## 4. How does the prototype chain affect the output of a `for...in` loop with enumerable properties?

The `for...in` loop iterates over all **enumerable properties** found **on the object itself as well as those inherited from its prototype chain**.  
This means:

- If the object's prototype (or any prototype up the chain) has enumerable properties, they **will be included** in the iteration.
- This can sometimes lead to unexpected properties showing up when iterating with `for...in`.

#### Example:
```javascript
const proto = { inheritedProp: "value" };
Object.defineProperty(proto, "hiddenProp", {
  value: "hidden",
  enumerable: false
});

const obj = Object.create(proto);
obj.ownProp = "own";

for (let key in obj) {
  console.log(key); 
  // Outputs:
  // "ownProp"
  // "inheritedProp"  (because it's enumerable in prototype)
}
```
## 5. Are class methods enumerable in ES6 classes? Why or why not?

No, **class methods in ES6 classes are not enumerable**.

- Methods defined inside a class are added to the class prototype with their `enumerable` attribute set to `false` by default.
- This design ensures that methods do **not** appear during property enumeration (e.g., in `for...in` loops), which keeps enumeration focused on instance-specific data properties.

#### Example:
```javascript
class MyClass {
  method() {
    return "Hello";
  }
}

const obj = new MyClass();

for (let key in obj) {
  console.log(key); // No output because methods are non-enumerable
}

console.log(Object.getOwnPropertyNames(MyClass.prototype)); 
// Output: ["constructor", "method"]
```

## Best Practices
## 6. When might you want to make a property non-enumerable?

You might want to make a property non-enumerable to:

- **Hide internal implementation details** or metadata from normal iteration.
- Prevent properties from appearing in loops like `for...in` or methods like `Object.keys()`.
- Avoid cluttering the output when enumerating over an object's properties.
- Protect sensitive or private data that should not be exposed during enumeration.

## 7. Why is it dangerous to assume `for...in` or `Object.keys()` will give all relevant data properties?

- `for...in` iterates over **enumerable own and inherited properties**, which can include unwanted properties from the prototype chain.
- `Object.keys()` returns **only enumerable own properties**, so it **excludes non-enumerable properties**.
- Both can miss **non-enumerable properties** that might be important.
- Assumptions that these methods provide a complete set of relevant properties can lead to bugs or security issues.

## 8. How do libraries typically hide internal or private properties using enumerability?

Libraries often define internal or private properties as **non-enumerable** by using `Object.defineProperty()` or similar methods with `enumerable: false`. This way:

- These properties do not appear in `for...in` loops or `Object.keys()`.
- They remain accessible internally but are hidden from users iterating over object properties.
- This helps encapsulate implementation details and reduce accidental misuse.

#### Example:
```javascript
const obj = {};

Object.defineProperty(obj, "_internalId", {
  value: 12345,
  enumerable: false
});

obj.publicName = "Visible";

console.log(Object.keys(obj)); // ["publicName"]
for (let key in obj) {
  console.log(key); // "publicName"
}

console.log(obj._internalId); // 12345 (accessible but hidden in enumeration)
```
## 9. Can making a property non-enumerable improve performance or maintainability?

**Yes, making a property non-enumerable can improve maintainability and, in some cases, performance:**

- **Maintainability:**
  - Hides internal or private properties from property enumerations (`for...in`, `Object.keys()`), reducing clutter.
  - Helps prevent accidental modification or misuse of internal data.
  - Encourages cleaner APIs by exposing only relevant properties to users.

- **Performance:**
  - While the performance impact is usually minimal, excluding non-enumerable properties from enumeration loops can reduce the number of iterations, potentially improving performance in large objects or complex enumerations.

Overall, using non-enumerable properties helps create clearer, more predictable object structures and safer code.
