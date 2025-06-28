# Objects
## 1. What is an object in JavaScript?

- An **object** in JavaScript is a collection of **key-value pairs** where keys (also called properties) are strings or symbols, and values can be any data type, including other objects.
- Objects are used to **store and organize data** and functionality.
- Almost everything in JavaScript (except primitives) is an object, including arrays and functions.

---

## 2. How do you create an object in JavaScript? List different ways.

There are several ways to create objects in JavaScript:

1. **Object Literal Syntax:**
   ```javascript
   const obj = {
     name: 'Alice',
     age: 25
   };
   ```

2. **Using the `new Object()` Constructor:**

    ```javascript
    const obj = new Object();
    obj.name = 'Alice';
    obj.age = 25;
    ```
3. **Using a Constructor Function:**
    ```js
    function Person(name, age) {
    this.name = name;
    this.age = age;
    }
    const person1 = new Person('Alice', 25);
    ```
4. **Using Object.create() method:**
    ```js
    const proto = { greet() { console.log('Hello'); } };
    const obj = Object.create(proto);
    obj.name = 'Alice';
    ```
5. **Using ES6 Classes (syntactic sugar for constructor functions):**
    ```js
    class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    }
    const person1 = new Person('Alice', 25);
    ```
## 3. What is the difference between object literals and constructor functions?

| Aspect                | Object Literals                     | Constructor Functions                  |
|-----------------------|-----------------------------------|--------------------------------------|
| Syntax                | Simple and concise `{ key: value }` | Function used with `new` keyword to create instances |
| Use case              | For creating a single object       | For creating multiple similar objects (instances) |
| Inheritance           | Directly creates an object         | Supports prototype-based inheritance |
| Reusability           | Less reusable                      | More reusable for creating multiple objects with shared structure |

**Summary:**  
Object literals are great for quickly creating single objects, while constructor functions are used when you need to create many objects of the same "type" or structure.

## 4. What are properties and methods in an object?

- **Properties** are key-value pairs that store data about the object. The key is a string or symbol, and the value can be any data type.
- **Methods** are functions that are stored as object properties. They define behaviors or actions that the object can perform.

**Example:**
```javascript
const person = {
  name: 'Alice',         // Property
  age: 30,               // Property
  greet: function() {    // Method
    console.log('Hello!');
  }
};
```
## 5. How can you access object properties? Explain dot notation vs bracket notation.

- **Dot notation** accesses properties using a literal name:

  ```javascript
  console.log(person.name);  // 'Alice'
  ```
  - Simple and readable.

  - Cannot be used if the property name is dynamic or not a valid identifier (e.g., contains spaces or starts with a number). 
- **Bracket notation accesses properties using a string key or an expression:**

    ```javascript
    console.log(person['name']);  // 'Alice'

    const prop = 'age';
    console.log(person[prop]);    // 30
    ```
    - Useful for dynamic property names.

    - Required if property names have special characters or spaces.


## 6. How can you add, update, or delete properties from an object?

- **Add or update properties** using dot notation or bracket notation:

  ```javascript
  person.city = 'New York';        // Add a new property
  person['age'] = 31;              // Update an existing property
  ```
- **Delete properties using the delete operator:**
    ```js
    delete person.city;
    ```
**Example:**
```js
const obj = { a: 1 };
obj.b = 2;           // Add property b
obj.a = 3;           // Update property a
delete obj.b;        // Delete property b
console.log(obj);    // { a: 3 }
```
## 7. What happens if you access a property that doesn't exist in an object?

- When you try to access a property that does **not exist** on an object, JavaScript returns `undefined`.
- This does **not** throw an error; it simply indicates the property is missing.

**Example:**
```javascript
const person = { name: 'Alice' };
console.log(person.age);  // Outputs: undefined (property 'age' does not exist)
```
## 8. How can you check if a property exists in an object?

There are several ways to check if a property exists:

### a) Using the `in` operator:
```javascript
'name' in person;   // true
'age' in person;    // false
```
### b) Using `hasOwnProperty()` method:
```javascript
person.hasOwnProperty('name');  // true
person.hasOwnProperty('age');   // false
```
This checks if the property exists directly on the object, not on its prototype chain.

### c) Checking for `undefined` (less reliable):
```javascript
if (person.age !== undefined) {
  // property exists (but could be set to undefined explicitly)
}
```
Note: The `in` operator and `hasOwnProperty()` are more reliable ways to check property existence than testing for `undefined`.
## 9. What does the `in` operator do in the context of objects?

- The `in` operator checks whether a given **property name exists in an object** or in its prototype chain.
- It returns `true` if the property exists, even if its value is `undefined`.

**Example:**
```javascript
const obj = { name: 'Alice', age: undefined };

console.log('name' in obj);   // true
console.log('age' in obj);    // true
console.log('gender' in obj); // false
```
## 10. How do you loop through all properties of an object?

There are several ways to iterate through properties:

### a) `for...in` loop:
- Loops over all **enumerable** properties, including those inherited through the prototype chain.

```javascript
const obj = { name: 'Alice', age: 25 };

for (let key in obj) {
  if (obj.hasOwnProperty(key)) {
    console.log(`${key}: ${obj[key]}`);
  }
}
```
### b) `Object.keys()` with `forEach()`

Returns an array of an object’s **own enumerable property names**.

```javascript
Object.keys(obj).forEach(key => {
  console.log(`${key}: ${obj[key]}`);
});
```
### c) `Object.entries()`

Returns an array of `[key, value]` pairs.

```javascript
for (const [key, value] of Object.entries(obj)) {
  console.log(`${key}: ${value}`);
}
```
### d) `Object.getOwnPropertyNames()`

Returns all **own properties** (including non-enumerable) of the object.

```javascript
Object.getOwnPropertyNames(obj).forEach(key => {
  console.log(`${key}: ${obj[key]}`);
});
```

## 11. What is `Object.keys()`, `Object.values()`, and `Object.entries()`?

These are built-in JavaScript methods used to retrieve different parts of an object:

### a) `Object.keys(obj)`
- Returns an array of the object's **own enumerable property names** (keys).
```javascript
const obj = { name: 'Alice', age: 25 };
console.log(Object.keys(obj));  // ['name', 'age']
```
### b) `Object.values(obj)`

Returns an array of the object's **own enumerable property values**.

```javascript
console.log(Object.values(obj));  // ['Alice', 25]
```
### c) `Object.entries(obj)`

Returns an array of the object's **own enumerable key-value pairs**, as arrays.

```javascript
console.log(Object.entries(obj));  // [['name', 'Alice'], ['age', 25]]
```

## 12. What is object destructuring? Provide an example.

**Object destructuring** is a syntax that allows you to **extract properties** from an object and assign them to variables in a concise way.

### Example:
```javascript
const user = {
  name: 'Alice',
  age: 25,
  city: 'New York'
};

// Destructuring
const { name, age } = user;

console.log(name); // 'Alice'
console.log(age);  // 25
```
**Renaming variables and setting default values:**
```js
const { name: userName, gender = 'Not specified' } = user;
console.log(userName); // 'Alice'
console.log(gender);   // 'Not specified'
```
## 13. How do you create nested objects and access their values?

A **nested object** is an object that contains another object as a property.

### Example:
```javascript
const person = {
  name: 'Alice',
  address: {
    city: 'New York',
    zip: 10001
  }
};

// Accessing nested values
console.log(person.address.city);  // 'New York'
console.log(person['address']['zip']);  // 10001
```
You can nest objects as deeply as needed and access values using dot or bracket notation.
## 14. What is the `this` keyword inside an object method?

In an **object method**, `this` refers to the object that the method is a property of — i.e., the object that is **calling** the method.

### Example:
```javascript
const user = {
  name: 'Alice',
  greet: function() {
    console.log(`Hello, my name is ${this.name}`);
  }
};

user.greet();  // Output: Hello, my name is Alice
```

**Notes:**

- If you use an arrow function as a method, `this` will not refer to the object but to the enclosing lexical scope.

- To ensure `this` refers to the correct object, use regular function expressions inside methods.
## 15. What is the difference between `==` and `===` when comparing objects?

- Both `==` (loose equality) and `===` (strict equality) **compare objects by reference**, not by their content.
- For objects, `==` and `===` behave the same way — they check if both operands **refer to the exact same object** in memory.
- Two different objects with identical properties are **not equal** with either operator.

### Example:
```javascript
const obj1 = { name: 'Alice' };
const obj2 = { name: 'Alice' };
const obj3 = obj1;

console.log(obj1 == obj2);   // false (different references)
console.log(obj1 === obj2);  // false (different references)
console.log(obj1 === obj3);  // true (same reference)
```
## 16. Are objects compared by value or by reference in JavaScript?

- **Objects are compared by reference** in JavaScript.
- This means two variables are equal only if they point to the **same object instance**.
- Even if two objects have identical properties and values, they are considered different if they are separate instances.

### Summary:
- Primitive types (`number`, `string`, etc.) are compared by **value**.
- Objects (including arrays and functions) are compared by **reference**.
## 17. How can you clone or copy an object? List shallow and deep copy methods.

### Shallow Copy
A shallow copy creates a new object but only copies the **top-level properties**. Nested objects are still referenced.

- **Using `Object.assign()`**:
  ```javascript
  const original = { a: 1, b: { c: 2 } };
  const copy = Object.assign({}, original);
  ```
- **Using Spread Syntax `{ ...obj }`:**
    ```js
    const original = { a: 1, b: { c: 2 } };
    const copy = { ...original };
    ```
### Deep Copy
A deep copy duplicates the object and all nested objects, so there are no shared references.

- **Using `JSON.parse(JSON.stringify(obj))`**  
  *(works only for simple data without functions, `undefined`, or symbols)*:

  ```javascript
  const original = { a: 1, b: { c: 2 } };
  const deepCopy = JSON.parse(JSON.stringify(original));
  ```
- **Using libraries like Lodash’s `_.cloneDeep()` for complex objects:**

    ```javascript
    const _ = require('lodash');
    const deepCopy = _.cloneDeep(original);
    ```



## 18. What is the difference between `Object.assign()` and spread syntax `{...obj}`?

| Feature                  | `Object.assign()`                        | Spread Syntax `{ ...obj }`             |
|--------------------------|----------------------------------------|---------------------------------------|
| Usage                    | `Object.assign(target, source)`         | `{ ...source }`                       |
| Mutability               | Modifies the **target** object          | Creates a **new** object              |
| Copies properties        | Copies enumerable own properties        | Copies enumerable own properties      |
| Shallow copy             | Yes                                    | Yes                                   |
| Can merge multiple objs  | Yes, can merge multiple source objects  | No, only copies one source object     |
| Syntax convenience       | Slightly more verbose                    | Cleaner, more concise                  |

### Example:
```javascript
const obj1 = { a: 1 };
const obj2 = { b: 2 };

// Object.assign
const merged1 = Object.assign({}, obj1, obj2);

// Spread syntax
const merged2 = { ...obj1, ...obj2 };
```
Both produce: `{ a: 1, b: 2 }`

### Summary:
- Both create **shallow copies** of objects.
- `Object.assign()` modifies a **target object**, while spread syntax creates a **new object**.
- Spread syntax is generally preferred for **clarity and brevity**.
## 19. What are getter and setter methods in objects? Provide an example.

**Getters and setters** are special methods in JavaScript objects that allow you to define how to **access** (get) and **modify** (set) a property. They help control the reading and writing of property values and can add additional logic during these operations.

### Example:

```javascript
const person = {
  firstName: 'Alice',
  lastName: 'Smith',
  
  // Getter for fullName
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },

  // Setter for fullName
  set fullName(name) {
    const parts = name.split(' ');
    this.firstName = parts[0];
    this.lastName = parts[1];
  }
};

console.log(person.fullName); // Outputs: Alice Smith

person.fullName = 'Bob Johnson';
console.log(person.firstName); // Outputs: Bob
console.log(person.lastName);  // Outputs: Johnson
```
## 20. How can you freeze or seal an object? What is the difference between `Object.freeze()` and `Object.seal()`?

### Object.freeze()
- Makes an object **immutable**.
- You **cannot add, delete, or modify** any properties after freezing.
- The object becomes **read-only**.

```javascript
const obj = { name: 'Alice' };
Object.freeze(obj);

obj.name = 'Bob';      // Fails silently or throws error in strict mode
obj.age = 30;          // Fails to add
delete obj.name;       // Fails to delete

console.log(obj);      // { name: 'Alice' }
```
### Object.seal()
Prevents adding or deleting properties but allows modification of existing properties.

The object is sealed, but its property values can still change.

```javascript
const obj = { name: 'Alice' };
Object.seal(obj);

obj.name = 'Bob';      // Allowed: property value modified
obj.age = 30;          // Fails to add new property
delete obj.name;       // Fails to delete property

console.log(obj);      // { name: 'Bob' }
```

### Summary of Differences:

| Feature           | `Object.freeze()`        | `Object.seal()`        |
|-------------------|--------------------------|------------------------|
| Add new properties | No                       | No                     |
| Delete properties  | No                       | No                     |
| Modify properties  | No                       | Yes                    |
| Makes object       | Completely immutable     | Sealed but mutable     |

## 21. What is a computed property in object literals? Give an example.

A **computed property** in an object literal allows you to use an expression (usually a variable or a calculation) as the property name by enclosing it in square brackets `[ ]`. This is useful when the property name is dynamic or not known until runtime.

### Example:

```javascript
const key = 'name';
const obj = {
  [key]: 'Alice',        // 'name' becomes the property key
  ['age' + 10]: 35       // 'age10' becomes the property key
};

console.log(obj); 
// Output: { name: 'Alice', age10: 35 }
```
## 22. Can object property names be symbols? Why would you use them?

Yes, object property names **can be symbols** in JavaScript.

### Why use symbols as property keys?

- **Uniqueness:** Symbols are guaranteed to be unique, preventing property name collisions, especially when integrating code from different sources or libraries.
- **Privacy:** Symbols can be used to create properties that are not easily accessible or accidentally overwritten, effectively serving as a form of private property.
- **Customization:** Some built-in JavaScript behaviors use well-known symbols (e.g., `Symbol.iterator`) to customize object behavior.

### Example:

```javascript
const sym = Symbol('uniqueKey');
const obj = {
  [sym]: 'secret value'
};

console.log(obj[sym]);  // Outputs: 'secret value'
```
## 23. How are objects used in JSON, and how do you convert objects to/from JSON?

JSON (JavaScript Object Notation) is a lightweight text format used to represent objects and data structures for storage or transmission.

### Converting an object to JSON:

Use `JSON.stringify()` to convert a JavaScript object into a JSON string.

```javascript
const obj = { name: 'Alice', age: 25 };
const jsonString = JSON.stringify(obj);

console.log(jsonString);  // '{"name":"Alice","age":25}'
```
### Converting JSON to an object:

Use `JSON.parse()` to convert a JSON string back into a JavaScript object.

```javascript
const jsonStr = '{"name":"Alice","age":25}';
const obj = JSON.parse(jsonStr);

console.log(obj.name);  // 'Alice'
```
### Notes:
- JSON supports only certain data types: strings, numbers, booleans, null, arrays, and objects.
- Functions, `undefined`, and symbols **cannot** be represented in JSON.
