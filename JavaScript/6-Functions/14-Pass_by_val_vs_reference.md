## 1. Does JavaScript use pass-by-value or pass-by-reference when passing arguments to functions?

JavaScript **always uses pass-by-value** when passing arguments to functions. However, **when a reference type** (like an object or array) is passed, the **value being passed is a reference to the object**, not the actual object itself. This often causes confusion and makes it appear as though JavaScript uses pass-by-reference for objects.

## 2. What is the key difference between passing primitive values and reference values to a function?

- **Primitive values** (like numbers, strings, booleans, `null`, `undefined`, `Symbol`, `BigInt`) are passed by value. The function gets a **copy** of the original value, and changes inside the function **do not affect** the original variable.

- **Reference values** (like objects, arrays, functions) are also passed by value — **but the value is a reference** (i.e., a memory address) to the object. This means that if you modify the object's contents inside the function, the changes **will affect** the original object.


## 3. Example: Modifying a parameter inside a function

```javascript
function modifyPrimitive(x) {
  x = x + 10;
  console.log("Inside function (primitive):", x);
}

function modifyObject(obj) {
  obj.value = obj.value + 10;
  console.log("Inside function (object):", obj);
}

let num = 5;
modifyPrimitive(num);
console.log("Outside function (primitive):", num); // Still 5

let myObj = { value: 5 };
modifyObject(myObj);
console.log("Outside function (object):", myObj); // { value: 15 }
```
**Explanation:**

- In the `modifyPrimitive` function, `num` remains unchanged outside the function because it's a primitive.

- In the `modifyObject` function, `myObj` is modified because the function operates on the same reference to the object.

## 4. What happens if you assign a new value to a parameter inside the function?

When you assign a **new value** to a parameter inside a function:

- For **primitive values**, it only changes the **local copy** of the parameter. The original value outside the function **remains unchanged**.
- For **reference values** (objects or arrays), if you **reassign** the parameter to a new object or array, it **breaks the reference** and no longer affects the original object.

#### Example:

```javascript
function reassignPrimitive(x) {
  x = 100;
  console.log("Inside function (primitive):", x);
}

function reassignObject(obj) {
  obj = { value: 100 };
  console.log("Inside function (reassigned object):", obj);
}

let num = 5;
reassignPrimitive(num);
console.log("Outside function (primitive):", num); // Still 5

let myObj = { value: 5 };
reassignObject(myObj);
console.log("Outside function (object):", myObj); // Still { value: 5 }
```
Reassigning the parameter does not affect the original object or primitive variable outside the function.
## 5. How can you prevent a function from modifying an object passed to it?

You can prevent a function from modifying an object in the following ways:

### 1. **Use `Object.freeze()`**

`Object.freeze()` makes an object **immutable** (but only shallowly). Any attempt to modify its properties will silently fail (or throw an error in strict mode).

```javascript
function safeFunction(obj) {
  obj.value = 20; // This will not change the original object
}

const frozenObj = Object.freeze({ value: 10 });
safeFunction(frozenObj);
console.log(frozenObj); // Output: { value: 10 }
```
Note: `Object.freeze()` does not deep-freeze nested objects.
### 2. **Pass a copy of the object (shallow copy)**
Create a shallow copy of the object using the spread operator (...) or Object.assign(), then pass the copy to the function.

```javascript
function safeFunction(obj) {
  obj.value = 20;
  console.log("Modified inside function:", obj);
}

const original = { value: 10 };
const copy = { ...original }; // Shallow copy
safeFunction(copy);
console.log("Original object:", original); // Output: { value: 10 }
```
### 3. **Use deep cloning for nested objects**
If the object has nested structures, use deep cloning methods such as:

- `structuredClone()` (built-in, modern browsers)

- `JSON.parse(JSON.stringify(obj))` (works for simple data)

- Lodash’s `_.cloneDeep()` for complex cases

```javascript
const deepCopy = structuredClone(original);
safeFunction(deepCopy);
```
Deep cloning ensures no shared references between the original and the copy, so changes inside the function do not affect the original object.