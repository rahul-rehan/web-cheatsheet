## 1. What is shadowing in the context of prototype chains?

- **Shadowing** occurs when an object defines a property with the same name as one found in its prototype chain.
- The object's own property **"shadows"** or **overrides** the prototype property, making the prototype's version inaccessible via normal property access on that object.


## 2. What happens when a property is defined in both the object and its prototype?

- The object's own property **takes precedence** over the prototype's property.
- Accessing the property on the object returns the **own property value**, not the prototype's.
- The prototype property remains unchanged and accessible from other objects that don't shadow it.


## 3. How can you detect if a property is shadowing a prototype property?

You can check:

1. If the object has its **own property** using `hasOwnProperty()`:

```javascript
if (obj.hasOwnProperty('prop')) {
  console.log('Property is own property (could be shadowing).');
}
```
2. If the same property exists on the prototype:

```javascript
const proto = Object.getPrototypeOf(obj);
if (proto && proto.hasOwnProperty('prop')) {
  console.log('Property exists on prototype too — shadowing occurs.');
}
```
Combining both:

```javascript
if (obj.hasOwnProperty('prop') && Object.getPrototypeOf(obj)?.hasOwnProperty('prop')) {
  console.log('Property "prop" is shadowing a prototype property.');
}
```
## 4. What does `hasOwnProperty()` check for in an object?

- The `hasOwnProperty()` method checks whether an object has a **specific property as its own (not inherited)** property.
- It returns `true` if the property exists directly on the object, and `false` if the property is inherited through the prototype chain.

```javascript
const obj = { name: "Alice" };
console.log(obj.hasOwnProperty('name')); // true
console.log(obj.hasOwnProperty('toString')); // false (inherited from prototype)
```
## 5. Provide an example where method shadowing causes unexpected behavior.

```javascript
const proto = {
  greet() {
    console.log("Hello from prototype");
  }
};

const obj = Object.create(proto);

// Shadowing greet method
obj.greet = function() {
  console.log("Hello from object");
};

obj.greet(); // Output: "Hello from object" — shadows prototype method

// Later, code expecting the prototype's greet may behave differently due to shadowing
```
In this example, the object's own `greet` method overrides the prototype's version, which can cause unexpected behavior if the prototype method was expected to be called.
## 6. Can you shadow a built-in method like `toString()`? What are the implications?

- Yes, you can shadow built-in methods like `toString()` by defining them directly on an object.
- **Implications:**
  - Calls to `toString()` on that object will use the new method, which can change expected behavior.
  - This may cause confusion or bugs if other code expects the default `toString()` behavior.
  - It can be useful for customizing string representations but should be done carefully.

```javascript
const obj = {
  toString() {
    return "Custom toString output";
  }
};

console.log(obj.toString()); // "Custom toString output"
console.log(String(obj));    // "Custom toString output"
```
