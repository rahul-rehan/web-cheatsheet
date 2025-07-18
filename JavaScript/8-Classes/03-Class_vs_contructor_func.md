## 1. What are the key differences between ES6 classes and constructor functions?

- **Syntax:**  
  ES6 classes use a clean, declarative `class` syntax, while constructor functions use regular functions with manual prototype assignments.

- **Strict Mode:**  
  Code inside ES6 classes is automatically in strict mode; constructor functions are not unless you specify it.

- **Hoisting:**  
  Constructor functions are hoisted (can be called before declaration), but ES6 classes are **not hoisted** and must be declared before use.

- **Methods:**  
  In ES6 classes, methods are defined on the prototype by default and are non-enumerable; in constructor functions, methods need to be added explicitly to the prototype.

- **`new` enforcement:**  
  ES6 classes throw an error if called without `new`; constructor functions may silently fail or behave incorrectly if called without `new`.

- **Inheritance:**  
  ES6 classes use `extends` and `super()` for inheritance, providing clearer syntax; constructor functions require manual prototype chaining.

## 2. Are ES6 classes just syntactic sugar over constructor functions?

- **Yes, mostly.**  
  ES6 classes provide a cleaner, more intuitive syntax for the same prototypal inheritance model that constructor functions use under the hood.

- They do **not** introduce a new object model but wrap existing prototypal inheritance with better semantics.

## 3. How is this handled differently in ES6 classes vs constructor functions?

| Feature              | ES6 Classes                             | Constructor Functions                     |
|----------------------|---------------------------------------|------------------------------------------|
| Syntax               | `class` keyword                       | Function declaration                     |
| Method definitions   | Inside class body (non-enumerable)    | Added to `.prototype` manually           |
| Inheritance          | `extends` and `super()` keywords      | Manual prototype chain manipulation      |
| `this` initialization| `super()` must be called in subclass  | Usually `call` or `apply` to inherit     |
| Call without `new`   | Throws error                          | No error, may cause bugs                  |
| Hoisting             | Not hoisted                          | Hoisted                                  |
## 4. How is inheritance implemented in ES6 classes vs constructor functions?

- **ES6 Classes:**  
  Inheritance is implemented using the `extends` keyword to create a subclass and `super()` to call the parent class constructor. This provides clear and concise syntax for class inheritance.

  ```js
  class Parent {
    constructor(name) {
      this.name = name;
    }
  }

  class Child extends Parent {
    constructor(name, age) {
      super(name);
      this.age = age;
    }
  }
  ```
- **Constructor Functions:**

    Inheritance is implemented manually by setting up the prototype chain, usually by assigning Child.prototype = Object.create(Parent.prototype), and calling the parent constructor with .call() or .apply() inside the child constructor.

    ```js
    function Parent(name) {
    this.name = name;
    }

    function Child(name, age) {
    Parent.call(this, name);
    this.age = age;
    }

    Child.prototype = Object.create(Parent.prototype);
    Child.prototype.constructor = Child;
    ```
## 5. Can you use Object.create() with ES6 classes? Why or why not?

- **Technically yes, but rarely needed:**  
  Since ES6 classes handle prototype chaining automatically via `extends`, you don't usually need to manually use `Object.create()` with ES6 classes.

- **Why:**  
  `Object.create()` is a lower-level API to create objects with a specified prototype. ES6 classes abstract this complexity, making manual prototype manipulation unnecessary in typical class-based code.

- **Possible use case:**  
  If you want to create an object with the prototype of a class without calling the constructor, you could use `Object.create(SomeClass.prototype)`.

## 6. What is more readable or maintainable in large codebases: ES6 classes or custom types?

- **ES6 classes are generally more readable and maintainable in large codebases** because:  
  - They provide a standardized, clear syntax for defining types and inheritance.  
  - They are familiar to developers from other object-oriented languages.  
  - They help avoid manual prototype chain setup errors.  
  - Support tools and IDEs often have better support for ES6 classes (like autocomplete and static analysis).

- **Custom constructor functions with manual prototype manipulation** can be more error-prone and harder to understand, especially for developers unfamiliar with JavaScript’s prototypal inheritance.

- That said, **factory functions** and other patterns may sometimes be preferable for specific use cases like encapsulation or functional programming styles.
## 7. Which approach (class or constructor function) is preferable in modern JavaScript and why?

- **ES6 classes are generally preferable** in modern JavaScript because:  
  - They offer clearer, more concise, and standardized syntax.  
  - They simplify inheritance with `extends` and `super()`.  
  - They improve readability and maintainability.  
  - They align better with modern tooling and developer expectations.

- **Constructor functions** are still valid but considered more verbose and error-prone due to manual prototype handling.

## 8. Are ES6 class methods defined on the instance or on the prototype?

- **ES6 class methods are defined on the prototype**, not on each individual instance.  
- This means all instances share the same method definitions, saving memory and enabling inheritance.

## 9. How do you distinguish an ES6 class constructor from a traditional constructor function?

- **ES6 class constructors:**  
  - Use the `class` keyword.  
  - Must be called with `new`; calling without `new` throws an error.  
  - Methods are declared inside the class body.  
  - Are not hoisted like functions.

- **Traditional constructor functions:**  
  - Are regular functions used with `new`.  
  - Can be called without `new` (which may cause bugs).  
  - Prototype methods are added manually.  
  - Are hoisted as normal functions.
