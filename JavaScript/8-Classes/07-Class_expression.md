## 1. What is a class expression in JavaScript?

- A **class expression** is a way to define a class inside an expression, typically assigned to a variable.
- It can be anonymous or named.
- Class expressions are not hoisted, unlike class declarations.

## 2. How do class expressions differ from class declarations?

| Aspect              | Class Declaration                  | Class Expression                  |
|---------------------|----------------------------------|---------------------------------|
| Hoisting            | Hoisted (cannot be used before declaration, but known to the engine) | Not hoisted (cannot be used before definition) |
| Naming              | Must have a name                  | Can be anonymous or named        |
| Usage               | Standalone declaration            | Used as part of expressions or assigned to variables |


## 3. Provide an example of a named class expression

```js
const MyClass = class CustomName {
  constructor(value) {
    this.value = value;
  }

  show() {
    console.log(this.value);
  }
};

const instance = new MyClass(42);
instance.show();  // Output: 42

console.log(MyClass.name);        // "CustomName"
console.log(instance.constructor.name); // "CustomName"
```
## 4. Can a class expression be anonymous? Show syntax.

Yes, a class expression can be anonymous. Example syntax:

```js
const MyClass = class {
  constructor() {
    this.value = 10;
  }
};
```
Here, the class has no name and is assigned directly to `MyClass`.
## 5. What is the use of naming a class expression if the name is only available inside the class body?

- Naming a class expression allows **self-reference** within the class, enabling methods to refer to the class itself (e.g., for recursion).
- It improves **debugging** by providing a meaningful name in stack traces and error messages.
- The name is **local to the class body** and does not create a variable in the outer scope, preventing scope pollution.

Example:

```js
const MyClass = class CustomName {
  method() {
    console.log(CustomName.name); // Outputs: "CustomName"
  }
};
```
## 6. Can you assign a class expression to a variable or pass it as a parameter?

- Yes, class expressions can be assigned to variables just like any other value.

```js
const MyClass = class {
  constructor() {
    console.log('Instance created');
  }
};
const instance = new MyClass();
```
- You can also pass class expressions as function parameters:

```js
function createInstance(ClassExpr) {
  return new ClassExpr();
}

const instance = createInstance(class {
  constructor() {
    console.log('Instance from parameter class');
  }
});
```
- This flexibility makes class expressions useful for dynamic class creation and modular code.
## 7. What is the return value of a class expression?

- A class expression evaluates to the class itself (the constructor function), which can be assigned to variables or passed around.

## 8. Can class expressions be used conditionally or inline in expressions? Provide an example.

- Yes, class expressions can be defined and used inline or conditionally, enabling dynamic class definitions.

**Example:**

```js
const createClass = (useExtended) => {
  return useExtended
    ? class Extended {
        greet() { return "Hello from Extended"; }
      }
    : class Basic {
        greet() { return "Hello from Basic"; }
      };
};

const MyClass = createClass(true);
const instance = new MyClass();
console.log(instance.greet()); // "Hello from Extended"
```
- This pattern allows defining classes on the fly based on runtime conditions.