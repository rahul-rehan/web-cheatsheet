## 1. What are accessor properties in JavaScript?

Accessor properties are properties defined by getter and/or setter functions instead of a fixed value. They allow custom logic to be executed when a property is accessed (get) or assigned a value (set). These properties are useful for creating dynamic, computed, or validated properties in objects.

## 2. How do you define a getter and a setter in an object literal?

You can define a getter and setter using the `get` and `set` keywords within an object literal:

```javascript
const person = {
  firstName: 'Alice',
  lastName: 'Smith',
  
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },
  
  set fullName(name) {
    const parts = name.split(' ');
    this.firstName = parts[0];
    this.lastName = parts[1];
  }
};

console.log(person.fullName); // "Alice Smith"
person.fullName = 'Bob Johnson';
console.log(person.firstName); // "Bob"
```
## 3. Can a property be both a data property and an accessor property at the same time?

No, a property cannot be both a **data property** and an **accessor property** at the same time.

In JavaScript:

- A **data property** uses a `value` and `writable` attribute.
- An **accessor property** uses `get` and/or `set` functions.

If you try to define both types for the same property, it results in an error. You must choose one or the other for a given property.
## 4. Example of an Object with a Computed Value Using a Getter

```javascript
const rectangle = {
  width: 10,
  height: 5,
  
  get area() {
    return this.width * this.height;
  }
};

console.log(rectangle.area); // 50 (computed dynamically)
```
In this example, `area` is a computed property that calculates the rectangle's area whenever accessed, based on the current `width` and `height`.
## 5. What is the Use of Setters in Encapsulating Object State?

Setters allow controlled updates to an object's properties and are useful for:

- **Validating input values** before storing them
- **Encapsulating internal logic**, so the internal structure can change without affecting external code
- **Triggering side effects**, such as logging or updating related properties

Example:

```javascript
const user = {
  _age: 0,

  set age(value) {
    if (value >= 0) {
      this._age = value;
    } else {
      console.warn('Age must be non-negative');
    }
  },

  get age() {
    return this._age;
  }
};

user.age = 25;    // sets _age to 25
console.log(user.age); // 25

user.age = -5;    // Warning: Age must be non-negative
console.log(user.age); // 25
```
Setters encapsulate logic, helping enforce constraints and maintain data integrity.