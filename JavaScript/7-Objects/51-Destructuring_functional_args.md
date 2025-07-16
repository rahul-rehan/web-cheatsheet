## 1. How can you destructure an object directly in a function's parameter list?

You can destructure an object right in the function’s parameter list by specifying the destructuring pattern inside the parentheses.

## 2. What are the advantages of using destructuring in function arguments?

- **Simplifies code** by extracting only needed properties directly.
- **Provides default values** easily for missing or undefined properties.
- **Improves readability** by clearly showing expected properties.
- **Avoids repetitive access** to object properties inside the function.

## 3. Provide an example of a function that destructures its parameter and uses default values.

```javascript
function greet({ name = 'Guest', age = 30 } = {}) {
  console.log(`Hello, ${name}! You are ${age} years old.`);
}

greet({ name: 'Alice', age: 25 }); // Hello, Alice! You are 25 years old.
greet({ name: 'Bob' });             // Hello, Bob! You are 30 years old.
greet();                           // Hello, Guest! You are 30 years old.
```
#### In this example:

- The function `greet` destructures `name` and `age` from the parameter object.

- Default values are provided for both `name` and `age`.

- The entire parameter has a default value of `{}` to handle the case when no argument is passed.
## 4. Can you destructure nested properties in function parameters?

Yes, you can destructure nested properties directly within function parameters by using nested curly braces that mirror the structure of the object.

#### Example:

```javascript
function displayUser({ name, address: { city, zip } }) {
  console.log(`${name} lives in ${city}, ZIP code ${zip}.`);
}

const user = {
  name: 'John',
  address: {
    city: 'New York',
    zip: '10001'
  }
};

displayUser(user); // John lives in New York, ZIP code 10001.
```
## 5. How do you provide default values for the entire destructured object parameter?

You can assign a default empty object `{}` as the default value for the entire parameter to handle cases when the argument is `undefined` or not passed.

#### Example:

```javascript
function greet({ name = 'Guest' } = {}) {
  console.log(`Hello, ${name}!`);
}

greet(); // Hello, Guest!
greet({ name: 'Alice' }); // Hello, Alice!
```

## Advanced Scenarios & Best Practices
## 1. Can object destructuring be used with the rest syntax? Provide an example.

Yes, object destructuring supports the rest syntax (`...rest`) to collect the remaining properties that are not explicitly destructured.

#### Example:

```javascript
const user = {
  name: 'Alice',
  age: 28,
  email: 'alice@example.com',
  city: 'New York'
};

const { name, age, ...rest } = user;

console.log(name); // Alice
console.log(age);  // 28
console.log(rest); // { email: 'alice@example.com', city: 'New York' }
```
## 2. How do you extract only a few properties while leaving the rest in another object?

By destructuring the desired properties and using the rest syntax to gather the remaining properties into a new object.

#### Example:

```javascript
const { name, age, ...others } = user;
```
Here, `name` and `age` are extracted, while all other properties are stored in `others`.
## 3. What are common use cases for destructuring in real-world applications?

- **Extracting configuration options** from objects passed as function arguments.  
- **Reading specific fields** from API responses or JSON data.  
- **Swapping variables** without a temporary variable.  
- **Handling default values** easily for missing properties.  
- **Splitting data into relevant and irrelevant parts**, such as separating metadata from content.  
- **Simplifying access** to deeply nested properties in complex objects.  
## 4. When should destructuring be avoided for readability?

- When the object structure is very complex or deeply nested, making the destructuring syntax hard to follow.
- When variable names in the destructuring pattern become unclear or ambiguous.
- When destructuring causes too many variables to be declared at once, cluttering the scope.
- When the destructuring statement spans multiple lines and reduces code clarity.
- In cases where explicit property access (e.g., `obj.prop`) makes the code easier to understand for the team or less experienced developers.

## 5. How does destructuring improve code readability and reduce boilerplate?

- It allows concise extraction of multiple properties from objects in a single statement.
- Reduces repetitive code like multiple lines of `const var = obj.prop`.
- Makes it clear which properties are being used from an object upfront.
- Supports default values and renaming inline, simplifying function parameters and assignments.
- Enhances maintainability by minimizing code verbosity and clarifying intent.
