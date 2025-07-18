## 1. What are getters and setters in JavaScript?

- **Getters** are special methods that get the value of a property.  
- **Setters** are special methods that set the value of a property.  
- They allow you to define custom behavior when properties are accessed or modified.

## 2. How do getters and setters help with encapsulation in JavaScript?

- They allow controlling access to an object's properties, enabling validation, computed properties, or side effects.  
- They hide the internal representation and provide a clean interface to interact with object data.

## 3. What is the syntax for defining a getter in an object literal?

```js
const obj = {
  get propertyName() {
    // return the computed or stored value
    return 'value';
  }
};
```
## 4. What is the syntax for defining a setter in an object literal?

```js
const obj = {
  set propertyName(value) {
    // handle the value being set
  }
};
```
## 5. Example of an object using both a getter and a setter

```js
const person = {
  firstName: "John",
  lastName: "Doe",
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },
  set fullName(name) {
    const parts = name.split(" ");
    this.firstName = parts[0] || "";
    this.lastName = parts[1] || "";
  }
};

console.log(person.fullName); // John Doe
person.fullName = "Jane Smith";
console.log(person.firstName); // Jane
console.log(person.lastName);  // Smith
```
## 6. How does a getter differ from a regular method?

- A **getter** is accessed like a property, without parentheses.  
- A **regular method** must be called with parentheses `()`.

**Example:**

```js
const obj = {
  get value() {
    return 42;
  },
  valueMethod() {
    return 42;
  }
};

console.log(obj.value);       // 42  (accessed like a property)
console.log(obj.valueMethod()); // 42  (called like a function)
```
- Getters provide a way to access computed or derived values transparently, improving encapsulation and usability.
## 7. What is the purpose of a setter function in JavaScript objects?

A **setter** function allows you to define custom behavior when a property value is assigned or updated on an object. It enables:

- **Controlled property assignment:** Validate or transform data before setting the property.
- **Encapsulation:** Hide internal details and control how values are updated.
- **Side effects:** Perform additional actions automatically when a property changes (e.g., logging, updating related state).

**Example:**

```js
const person = {
  _age: 0,
  set age(value) {
    if (value < 0) {
      console.error("Age cannot be negative");
    } else {
      this._age = value;
    }
  },
  get age() {
    return this._age;
  }
};

person.age = 25;  // Sets age to 25
person.age = -5;  // Logs error, does not update
```