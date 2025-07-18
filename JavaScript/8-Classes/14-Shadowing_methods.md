## 1. What does it mean to shadow a method in JavaScript class inheritance?

Shadowing a method means that a subclass defines a method with the same name as a method in its parent class, effectively overriding or hiding the parent’s version of that method.

## 2. What happens if a subclass defines a method with the same name as a method in the parent class?

If a subclass defines a method with the same name, the subclass’s method overrides the parent class’s method. When the method is called on an instance of the subclass, the subclass’s version is executed instead of the parent’s.

## 3. How can you call a shadowed method from the parent class inside the overridden method?

You can call the parent class’s shadowed method using the `super` keyword inside the subclass method.

```js
class Parent {
  greet() {
    console.log("Hello from Parent");
  }
}

class Child extends Parent {
  greet() {
    super.greet(); // Calls Parent's greet method
    console.log("Hello from Child");
  }
}

const c = new Child();
c.greet();
// Output:
// Hello from Parent
// Hello from Child
```
## 4. Provide an example of method shadowing in a subclass.

```js
class Animal {
  speak() {
    console.log("Animal speaks");
  }
}

class Dog extends Animal {
  speak() {
    console.log("Dog barks");
  }
}

const dog = new Dog();
dog.speak(); // Output: "Dog barks"
```
In this example, the `Dog` class shadows the `speak` method inherited from `Animal` by providing its own implementation.
## 5. What are the implications of shadowing inherited methods in a large codebase?

- **Readability & Maintenance:** Shadowing can make it harder to understand which method implementation is executed, especially in deep or complex class hierarchies.
- **Unexpected Behavior:** Developers might assume the parent class method runs, causing bugs if the subclass method overrides it without clear indication.
- **Debugging Complexity:** Finding where methods are overridden can slow down debugging and increase cognitive load.
- **Code Duplication:** Shadowing sometimes leads to duplicated code if the subclass method largely replicates the parent's behavior without calling `super`.
- **Design Concerns:** Excessive method shadowing might suggest poor class design, where composition could be more appropriate than inheritance.
