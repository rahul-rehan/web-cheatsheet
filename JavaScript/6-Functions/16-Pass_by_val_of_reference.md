## 1. What are reference types in JavaScript?

In JavaScript, **reference types** are values that are not stored directly in the variable, but rather as a reference (or memory address) to the actual data.

Common reference types include:

- **Object**
- **Array**
- **Function**
- **Date**, **RegExp**, and other built-in object types

These types are stored and passed by **reference**, meaning the variable holds a reference (pointer) to the data in memory, not the data itself.


## 2. What happens when an object or array is passed to a function?

When an object or array is passed to a function:

- JavaScript passes the **reference** to the object/array, not a copy of the object itself.
- This means the function receives access to the **same object in memory**.
- As a result, any changes made to the object's properties or array elements **inside the function** will **affect the original object or array** outside the function.


## 3. Can a function modify the contents of an object or array passed to it?

**Yes**, a function **can modify** the contents of an object or array passed to it.

Since the function receives a reference to the same memory location, modifying the object or array’s properties or elements will be reflected outside the function.

#### Example:

```javascript
function updateObject(obj) {
  obj.name = "Updated";
}

const myObj = { name: "Original" };
updateObject(myObj);
console.log(myObj); // Output: { name: "Updated" }
```
**Explanation:**
- `myObj` is passed to the `updateObject` function.

- The function modifies the `name` property of the object.

- Since `obj` and `myObj` point to the same object in memory, the change is reflected outside the function.

This behavior only applies when modifying the contents. If you reassign the parameter to a new object inside the function, it will not affect the original object.
## 4. What happens if the function reassigns the parameter (e.g., `param = {}`)? Does it affect the original reference?

If a function **reassigns** a parameter to a new object (e.g., `param = {}`), it **does not** affect the original reference outside the function.

- The reassignment only changes the local copy of the reference inside the function.
- The original variable still points to the original object.

#### Example:

```javascript
function resetObject(obj) {
  obj = {}; // Reassigns to a new object (local to the function)
}

const myObj = { key: "value" };
resetObject(myObj);
console.log(myObj); // Output: { key: "value" }
```
The original object remains unchanged because the function only reassigns its local reference.
## 5. Give an example where modifying an array inside a function affects the original array

When an **array** is passed to a function, the function receives a **reference** to the original array. Therefore, changes made to the array inside the function **will affect** the original array outside the function.

#### Example:

```javascript
function addElement(arr) {
  arr.push(4);
}

const numbers = [1, 2, 3];
addElement(numbers);
console.log(numbers); // Output: [1, 2, 3, 4]
```
Explanation:
- The `numbers` array is passed to the `addElement` function.

- The function uses `push()` to add a new element to the array.

- Since arrays are reference types, the `arr` parameter refers to the same memory location as `numbers`.

- As a result, the original `numbers` array is modified.

This shows that functions can mutate arrays (or objects) passed to them by reference.

## 6. Can you clone an object to avoid mutation when passing to a function? How?

**Yes**, you can clone an object before passing it to a function to **prevent the original object from being mutated**. By working with a **copy** of the object, changes inside the function will not affect the original.


### Ways to clone an object:

#### 1. **Shallow copy using spread syntax (`...`)**

```javascript
const original = { name: "John" };
const copy = { ...original };
```
#### 2. **Shallow copy using Object.assign()**
```javascript
const copy = Object.assign({}, original);
```
Both spread syntax and `Object.assign()` create shallow copies, which only clone the top-level properties. Nested objects will still be copied by reference.
#### 3. **Deep copy for nested objects**
- Using `structuredClone()` (modern and built-in):

```javascript
const deepCopy = structuredClone(original);
```
- Using `JSON.parse(JSON.stringify(obj))` (for simple data):

```javascript
const deepCopy = JSON.parse(JSON.stringify(original));
```
Deep copies ensure that even nested objects are cloned, breaking all references to the original data structure.

**Example:**
```javascript
function modify(obj) {
  obj.name = "Modified";
}

const original = { name: "Original" };
modify({ ...original }); // Pass a shallow copy
console.log(original); // Output: { name: "Original" }
```
In this example, the original object remains unchanged because a copy was passed to the function.