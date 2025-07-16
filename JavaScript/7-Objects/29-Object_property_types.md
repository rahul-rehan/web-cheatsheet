## 1. What are the two types of properties in JavaScript objects?

JavaScript objects have two main types of properties:

1. **Data Properties**  
2. **Accessor Properties**


## 2. What is a data property in JavaScript?

A **data property** is a property that has a **value** and associated attributes:

- `value`: The actual data stored in the property.  
- `writable`: Whether the property value can be changed.  
- `enumerable`: Whether the property shows up during enumeration (e.g., in `for...in` loops).  
- `configurable`: Whether the property descriptor can be changed or the property can be deleted.

**Example:**

```js
const obj = { name: "Alice" };
// 'name' is a data property with the value "Alice"
```
## 3. What is an accessor property in JavaScript?

An **accessor property** is a property defined by a pair of getter and/or setter functions instead of a direct value. It allows you to run custom code when a property is read or written.

- **Getter**: A function that is called when the property is accessed.
- **Setter**: A function that is called when the property is assigned a value.

Accessor properties do not store a value themselves but compute or control the property’s value dynamically.

**Example:**

```js
const obj = {
  _name: 'Alice',
  get name() {
    return this._name.toUpperCase();
  },
  set name(value) {
    this._name = value.trim();
  }
};

console.log(obj.name); // Output: ALICE
obj.name = '  Bob  ';
console.log(obj.name); // Output: BOB
```
Here, `name` is an accessor property with getter and setter controlling access to the internal `_name` data property.
## 4. How do data and accessor properties differ in behavior and use cases?

| Aspect            | Data Property                          | Accessor Property                      |
|-------------------|--------------------------------------|--------------------------------------|
| **Stores Value**  | Stores a fixed value directly         | Computes or controls the value via getter/setter functions |
| **Usage**         | Simple property holding data          | Dynamic or computed properties, validation, side effects on access or assignment |
| **Syntax**        | Normal property assignment (`obj.prop = value`) | Defined via `get` and `set` functions |
| **Attributes**    | Has `value` and `writable` attributes | Has `get` and `set` functions, no direct value |
| **Example Use Case** | Holding user data                      | Calculating derived data, validation, lazy evaluation |

---

In summary, **data properties** hold actual data, while **accessor properties** allow more control and dynamic behavior when accessing or setting a property.
