## 1. How do you expose private fields using a getter method?

You can expose a private field by defining a public getter method in the class that returns the value of the private field.

## 2. How do you modify a private field using a setter method?

You can modify a private field by defining a public setter method in the class that assigns a new value to the private field.

## 3. Example of a class with a private field and corresponding getter/setter

```javascript
class Person {
  #name; // private field

  constructor(name) {
    this.#name = name;
  }

  // Getter for private field
  get name() {
    return this.#name;
  }

  // Setter for private field
  set name(newName) {
    this.#name = newName;
  }
}

const person = new Person("Alice");
console.log(person.name); // Output: Alice

person.name = "Bob";
console.log(person.name); // Output: Bob
```
## 4. Can getters/setters be used to add validation for private fields?

Yes, getters and setters can include validation logic to control how private fields are accessed or modified. For example, a setter can check the input value before assigning it to the private field, helping enforce constraints or business rules.

## 5. Should you always expose private fields via getters/setters? Why or why not?

Not necessarily. While getters and setters provide controlled access to private fields, exposing every private field might break encapsulation or lead to unintended side effects. It’s best to expose only those fields that need to be accessed or modified externally, keeping others fully private to maintain internal integrity and reduce coupling.
