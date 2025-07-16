## 1. What is a factory function in JavaScript?

A **factory function** is a regular function that **creates and returns a new object** each time it is called. It encapsulates the object creation logic and can set up properties and methods on the new object without using the `new` keyword.

```javascript
function createPerson(name, age) {
  return {
    name,
    age,
    greet() {
      console.log(`Hello, my name is ${name}`);
    }
  };
}

const person1 = createPerson('Alice', 30);
person1.greet(); // Hello, my name is Alice
```
## 2. How does a factory function differ from a constructor function?

| Aspect           | Factory Function                                   | Constructor Function                        |
|------------------|---------------------------------------------------|---------------------------------------------|
| Syntax           | Regular function that returns an object           | Function intended to be called with `new`  |
| Object creation  | Explicitly returns a new object                     | `new` keyword automatically creates `this`|
| Usage            | Called like a normal function                        | Called with `new` keyword                    |
| `this` binding   | Does not rely on `this`                             | Uses `this` to assign properties            |
| Inheritance      | Can use closures or `Object.create` for sharing    | Uses prototype chain for inheritance        |

**Example Constructor Function:**

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.greet = function() {
  console.log(`Hello, my name is ${this.name}`);
};

const person = new Person('Bob', 25);
person.greet();
```
## 3. What are the benefits of using factory functions over constructor functions?

- **No need to use `new`:** Factory functions avoid mistakes related to forgetting the `new` keyword, which can lead to incorrect `this` binding.
- **Encapsulation:** They can leverage closures to create private variables and methods, providing better data hiding.
- **Flexibility:** Factory functions are easier to customize and extend without relying on prototype inheritance.
- **Simpler syntax:** They have a more straightforward and intuitive syntax compared to constructor functions.
- **Avoid prototype pitfalls:** Since objects are created explicitly, it's easier to control inheritance and avoid issues related to prototype chains.

> **Note:** One potential downside is that factory functions might use more memory if methods are recreated for each instance rather than shared via prototypes.
## 4. Provide a simple example of a factory function that returns an object.

```javascript
function createUser(name, age) {
  return {
    name,
    age,
    greet() {
      console.log(`Hello, my name is ${name}`);
    }
  };
}

const user1 = createUser('Alice', 28);
user1.greet(); // Hello, my name is Alice
```
## 5. Can factory functions return new objects each time they are called? Why is this useful?

Yes, factory functions return a **new, independent object** every time they are called. This is useful because:

- Each object maintains its own separate state without interference.
- It avoids shared mutable state bugs.
- Allows creating multiple instances with different data easily.
## 6. How do factory functions support encapsulation and private data?

Factory functions support encapsulation by using **closures** to create private variables and methods that are not accessible outside the function scope. This allows sensitive data to be hidden from external access, exposing only the intended interface.

#### Example:

```javascript
function createCounter() {
  let count = 0; // private variable

  return {
    increment() {
      count++;
      return count;
    },
    getCount() {
      return count;
    }
  };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.getCount());  // 1
// 'count' is not accessible directly from outside the factory function
```
## 7. Can factory functions create methods inside the returned object? Show an example.

Yes, factory functions can create and return methods inside the objects they generate.

#### Example:

```javascript
function createCar(make, model) {
  return {
    make,
    model,
    start() {
      console.log(`${this.make} ${this.model} is starting.`);
    }
  };
}

const car = createCar('Toyota', 'Corolla');
car.start(); // Toyota Corolla is starting.
```
## 8. What are some use cases where factory functions are preferred?

- **Creating multiple instances with encapsulated private data:** Using closures to maintain private state.
- **Avoiding the complexities of `this` and `new`:** Factory functions don’t require `new` and avoid issues with incorrect `this` binding.
- **Dynamic object creation:** When you want to customize object creation logic easily.
- **Functional programming style:** When immutability and pure functions are preferred.
- **Module pattern implementations:** To encapsulate functionality and expose public APIs.
- **Avoiding prototype inheritance pitfalls:** When prototype inheritance is unnecessary or unwanted.
