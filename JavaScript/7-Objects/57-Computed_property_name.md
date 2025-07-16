## 1. What are computed property names in JavaScript object literals?

Computed property names allow you to dynamically define the names of object properties using expressions inside square brackets (`[]`) within an object literal.

This is useful when the property name is not known until runtime or is stored in a variable.

## 2. How do you define a computed property name using square brackets?

To define a computed property, wrap the expression that evaluates to the property name inside square brackets within the object literal:

```javascript
const key = "name";
const obj = {
  [key]: "Alice"
};
```
## 3. Provide an example of dynamically naming a property using a variable

```javascript
const propName = "age";
const user = {
  name: "Bob",
  [propName]: 30
};

console.log(user); // { name: "Bob", age: 30 }
```
In this example, the property name `age` is assigned dynamically using the value of the `propName` variable.
## 4. Can you use expressions as property names in computed properties?

Yes, you can use any valid JavaScript expression inside square brackets as a computed property name. The expression is evaluated at runtime to determine the key.

#### Example:

```javascript
const prefix = "user";
const obj = {
  [prefix + "Id"]: 101
};

console.log(obj.userId); // Output: 101
```
## 5. How does JavaScript evaluate computed property names at runtime?

JavaScript evaluates the expression inside the square brackets (`[]`) at the time the object is created. The resulting value is then used as the property name.

- If the expression evaluates to a **string** or **number**, it becomes a standard property key.
- If the expression evaluates to a **symbol**, it becomes a symbol-keyed property.

#### Example:

```javascript
const suffix = "Id";
const obj = {
  ["user" + suffix]: 123
};

console.log(obj.userId); // Output: 123
```
This shows how JavaScript dynamically computes the property name `"userId"` at runtime.
## 6. Are computed property names allowed in object destructuring or classes?

- **Object destructuring:**  
  Computed property names are **not allowed** directly in the left-hand side pattern of destructuring. You must use the actual property names.
  #### Example:

```javascript
const key = "age";
const user = { age: 25 };
// ❌ This will cause an error
// const { [key]: value } = user;
```
#### However, you can destructure dynamically using a workaround:

```javascript
const key = "age";
const user = { age: 25 };
const value = user[key];
```

- **Classes:**  
  Computed property names **are allowed** in class definitions to define methods or properties dynamically.

#### Example in classes:

```javascript
const methodName = "sayHello";

class Greeter {
  [methodName]() {
    console.log("Hello!");
  }
}

const g = new Greeter();
g.sayHello(); // Output: Hello!
```
#### In summary:

- Computed property names can be used in object literals and classes.

- They cannot be used directly in object destructuring patterns.