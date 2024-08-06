# Built In Objects

### 1. What are the different ways to create objects in JavaScript?

There are several ways to create objects in JavaScript:

1. **Object Literals:** The simplest way to create an object using curly braces `{}`.

   **Example:**
   ```javascript
   const person = {
       name: 'Alice',
       age: 25
   };
   ```

2. **Constructor Functions:** Create objects using a constructor function and the `new` keyword.

   **Example:**
   ```javascript
   function Person(name, age) {
       this.name = name;
       this.age = age;
   }

   const person = new Person('Bob', 30);
   ```

3. **ES6 Classes:** Use class syntax to define and create objects.

   **Example:**
   ```javascript
   class Person {
       constructor(name, age) {
           this.name = name;
           this.age = age;
       }
   }

   const person = new Person('Carol', 28);
   ```

4. **Object.create():** Create an object with a specified prototype object and properties.

   **Example:**
   ```javascript
   const proto = {
       greet() {
           console.log('Hello');
       }
   };

   const person = Object.create(proto);
   person.name = 'David';
   person.greet();  // Output: Hello
   ```

5. **Factory Functions:** Functions that return new object instances.

   **Example:**
   ```javascript
   function createPerson(name, age) {
       return {
           name: name,
           age: age
       };
   }

   const person = createPerson('Eve', 35);
   ```

### 2. Explain the difference between dot notation and bracket notation when accessing object properties.

- **Dot Notation:** Access properties using a dot (`.`) followed by the property name. Suitable for property names that are valid identifiers and known in advance.

   **Example:**
   ```javascript
   const person = {
       name: 'Alice',
       age: 25
   };

   console.log(person.name); // Output: Alice
   ```

- **Bracket Notation:** Access properties using brackets (`[]`) with the property name as a string. Useful for property names that are dynamic, not valid identifiers, or contain special characters.

   **Example:**
   ```javascript
   const person = {
       'full name': 'Bob',
       age: 30
   };

   console.log(person['full name']); // Output: Bob

   const propName = 'age';
   console.log(person[propName]); // Output: 30
   ```

### 3. What is the purpose of prototypes in JavaScript's object model?

**Prototypes** in JavaScript are used to create inheritance and share properties and methods between objects. Each object has a prototype object from which it can inherit properties and methods. The prototype chain allows objects to access methods and properties defined on their prototype.

**Example:**
```javascript
function Animal(name) {
    this.name = name;
}

Animal.prototype.speak = function() {
    console.log(this.name + ' makes a noise.');
};

const dog = new Animal('Dog');
dog.speak(); // Output: Dog makes a noise.
```

In this example, the `speak` method is defined on `Animal.prototype`, so it is available to all instances of `Animal`.

### 4. How can you check if a variable is an object in JavaScript? (using `typeof` or `instanceof`)

- **`typeof` Operator:** Can be used to check if a variable is an object, but it will return "object" for both objects and arrays, and `null`.

   **Example:**
   ```javascript
   const obj = {};
   const arr = [];
   const num = 42;
   const nll = null;

   console.log(typeof obj === 'object'); // Output: true
   console.log(typeof arr === 'object'); // Output: true
   console.log(typeof num === 'object'); // Output: false
   console.log(typeof nll === 'object'); // Output: true (but null is not an object)
   ```

- **`instanceof` Operator:** Checks if a variable is an instance of a specific class or constructor function.

   **Example:**
   ```javascript
   const obj = {};
   const arr = [];
   
   console.log(obj instanceof Object); // Output: true
   console.log(arr instanceof Array); // Output: true
   console.log(arr instanceof Object); // Output: true (arrays are objects)
   ```

   Note that `instanceof` does not work for `null` and will return `false`.

### 5. Describe the difference between primitive data types and reference types in JavaScript.

- **Primitive Data Types:** Simple values that are immutable. They include `undefined`, `null`, `boolean`, `number`, `string`, and `symbol`. These values are copied by value.

   **Example:**
   ```javascript
   let a = 10;
   let b = a; // b is a copy of a

   a = 20;
   console.log(b); // Output: 10 (b remains unchanged)
   ```

- **Reference Types:** More complex objects that are mutable and include objects, arrays, and functions. These are copied by reference, meaning changes to one reference will affect all references to that object.

   **Example:**
   ```javascript
   const obj1 = { name: 'Alice' };
   const obj2 = obj1; // obj2 references the same object as obj1

   obj1.name = 'Bob';
   console.log(obj2.name); // Output: Bob (both obj1 and obj2 reflect the change)
   ```

### 6. Explain the functionalities of the `Math` object and some commonly used methods (e.g., `Math.floor`, `Math.random`).

The `Math` object provides various mathematical functions and constants.

- **`Math.floor(x)`**: Returns the largest integer less than or equal to `x`.

   **Example:**
   ```javascript
   console.log(Math.floor(4.7)); // Output: 4
   ```

- **`Math.random()`**: Returns a random floating-point number between 0 (inclusive) and 1 (exclusive).

   **Example:**
   ```javascript
   console.log(Math.random()); // Output: A random number between 0 and 1
   ```

- **`Math.ceil(x)`**: Returns the smallest integer greater than or equal to `x`.

   **Example:**
   ```javascript
   console.log(Math.ceil(4.1)); // Output: 5
   ```

- **`Math.max(a, b, c, ...)`**: Returns the largest of the zero or more numbers provided.

   **Example:**
   ```javascript
   console.log(Math.max(1, 2, 3, 4)); // Output: 4
   ```

- **`Math.min(a, b, c, ...)`**: Returns the smallest of the zero or more numbers provided.

   **Example:**
   ```javascript
   console.log(Math.min(1, 2, 3, 4)); // Output: 1
   ```

### 7. What are the use cases for the `Date` object? How do you create and manipulate dates in JavaScript?

The `Date` object is used to work with dates and times. Use cases include creating timestamps, scheduling tasks, and displaying dates and times in different formats.

**Creating a Date Object:**
```javascript
const now = new Date(); // Current date and time
const specificDate = new Date('2024-08-06T00:00:00Z'); // Specific date and time
```

**Manipulating Dates:**
```javascript
const date = new Date();

// Get components of the date
console.log(date.getFullYear()); // Output: Current year
console.log(date.getMonth());    // Output: Current month (0-11)
console.log(date.getDate());     // Output: Day of the month (1-31)
console.log(date.getHours());    // Output: Hours (0-23)

// Set components of the date
date.setFullYear(2025);
date.setMonth(11); // December
date.setDate(25);
console.log(date); // Output: Updated date

// Formatting a date
console.log(date.toDateString()); // Output: Date in a human-readable format
console.log(date.toISOString());  // Output: ISO format
```

### 8. How can you iterate over the properties of an object using a `for...in` loop? What are the limitations of this approach?

**Iterating Over Properties:**

The `for...in` loop iterates over enumerable properties of an object, including properties inherited through the prototype chain.

**Example:**
```javascript
const person = {
    name: 'Alice',
    age: 25
};

for (let key in person) {
    if (person.hasOwnProperty(key)) { // Check to exclude inherited properties
        console.log(key + ': ' + person[key]);
    }
}
// Output:
// name: Alice
// age: 25
```

**Limitations:**

1. **Includes Inherited Properties:** `for...in` iterates over properties in the prototype chain, not just the object's own properties.
2. **Non-Enumerable Properties:** Does not iterate over properties with the `enumerable` attribute set to `false`.
3. **Order of Iteration:** The order of iteration is not guaranteed and can vary across different environments.

To avoid iterating over inherited properties, use `hasOwnProperty()` within the loop, or use `Object.keys()`

### 9. Describe the `String` object and some methods for string manipulation (e.g., `toUpperCase`, `slice`, `indexOf`).

The `String` object represents a sequence of characters and provides various methods to manipulate and inspect strings.

**Common Methods:**

- **`toUpperCase()`**: Converts all characters in the string to uppercase.

   **Example:**
   ```javascript
   const str = 'hello world';
   console.log(str.toUpperCase()); // Output: HELLO WORLD
   ```

- **`slice(start, end)`**: Extracts a section of the string from `start` index to `end` index (not inclusive).

   **Example:**
   ```javascript
   const str = 'hello world';
   console.log(str.slice(0, 5)); // Output: hello
   ```

- **`indexOf(substring, fromIndex)`**: Returns the index of the first occurrence of `substring`, starting the search at `fromIndex`. Returns `-1` if not found.

   **Example:**
   ```javascript
   const str = 'hello world';
   console.log(str.indexOf('world')); // Output: 6
   ```

- **`trim()`**: Removes whitespace from both ends of the string.

   **Example:**
   ```javascript
   const str = '   hello world   ';
   console.log(str.trim()); // Output: 'hello world'
   ```

### 10. What are the built-in methods for working with arrays like `push`, `pop`, `concat`, and `slice`?

**Common Array Methods:**

- **`push(element1, element2, ...)`**: Adds one or more elements to the end of the array and returns the new length of the array.

   **Example:**
   ```javascript
   const arr = [1, 2, 3];
   arr.push(4, 5);
   console.log(arr); // Output: [1, 2, 3, 4, 5]
   ```

- **`pop()`**: Removes the last element from the array and returns it.

   **Example:**
   ```javascript
   const arr = [1, 2, 3];
   const lastElement = arr.pop();
   console.log(lastElement); // Output: 3
   console.log(arr); // Output: [1, 2]
   ```

- **`concat(array2, array3, ...)`**: Combines two or more arrays and returns a new array.

   **Example:**
   ```javascript
   const arr1 = [1, 2];
   const arr2 = [3, 4];
   const combined = arr1.concat(arr2);
   console.log(combined); // Output: [1, 2, 3, 4]
   ```

- **`slice(start, end)`**: Returns a shallow copy of a portion of the array from `start` index to `end` index (not inclusive).

   **Example:**
   ```javascript
   const arr = [1, 2, 3, 4, 5];
   const sliced = arr.slice(1, 4);
   console.log(sliced); // Output: [2, 3, 4]
   ```

### 11. Explain how you would deep copy an object in JavaScript (avoiding reference issues).

Deep copying creates a new object with the same properties and nested properties as the original object, without referencing the original object’s nested objects.

**Methods:**

- **Using JSON methods:**
   ```javascript
   function deepCopy(obj) {
       return JSON.parse(JSON.stringify(obj));
   }

   const original = { a: 1, b: { c: 2 } };
   const copy = deepCopy(original);

   copy.b.c = 3;
   console.log(original.b.c); // Output: 2 (original is unaffected)
   ```

   **Note:** This method does not handle functions, `undefined`, or special objects like `Date` or `RegExp`.

- **Using a recursive function:**
   ```javascript
   function deepCopy(obj) {
       if (obj === null || typeof obj !== 'object') return obj;

       if (Array.isArray(obj)) {
           return obj.map(deepCopy);
       }

       const copy = {};
       for (let key in obj) {
           if (obj.hasOwnProperty(key)) {
               copy[key] = deepCopy(obj[key]);
           }
       }
       return copy;
   }

   const original = { a: 1, b: { c: 2 } };
   const copy = deepCopy(original);

   copy.b.c = 3;
   console.log(original.b.c); // Output: 2 (original is unaffected)
   ```

### 12. How can you define and use getters and setters in JavaScript objects?

Getters and setters allow you to define custom behavior for reading and writing properties.

**Example:**
```javascript
const person = {
    firstName: 'John',
    lastName: 'Doe',
    
    get fullName() {
        return `${this.firstName} ${this.lastName}`;
    },
    
    set fullName(name) {
        [this.firstName, this.lastName] = name.split(' ');
    }
};

console.log(person.fullName); // Output: John Doe
person.fullName = 'Jane Smith';
console.log(person.firstName); // Output: Jane
console.log(person.lastName);  // Output: Smith
```

### 13. Describe the concept of object immutability and its benefits in JavaScript.

**Object Immutability** refers to the concept of making objects that cannot be changed after they are created. This is beneficial for various reasons:

- **Predictability:** Immutable objects ensure that data does not change unexpectedly, making the behavior of your code more predictable.
- **Debugging:** Easier to track changes and bugs, as objects do not change their state over time.
- **Functional Programming:** Immutable objects align with functional programming principles, making it easier to write pure functions and manage state.

**Example using `Object.freeze()`:**
```javascript
const obj = Object.freeze({ a: 1, b: 2 });

obj.a = 3; // This will not work because obj is frozen
console.log(obj.a); // Output: 1
```

### 14. What is the difference between `Object.freeze` and `Object.seal` methods?

- **`Object.freeze(obj)`**: Makes an object immutable. Properties cannot be added, removed, or modified, and the object cannot be extended.

   **Example:**
   ```javascript
   const obj = Object.freeze({ a: 1 });
   obj.a = 2; // No effect
   console.log(obj.a); // Output: 1
   ```

- **`Object.seal(obj)`**: Prevents adding or removing properties but allows modification of existing properties. The object cannot be extended.

   **Example:**
   ```javascript
   const obj = Object.seal({ a: 1 });
   obj.a = 2; // Allowed
   obj.b = 3; // Not allowed
   console.log(obj.a); // Output: 2
   console.log(obj.b); // Output: undefined
   ```

### 15. Explain the `hasOwnProperty` method and its use in object property access.

**`hasOwnProperty()`** is a method available on all objects that checks if the object has a specific property as its own (not inherited).

**Example:**
```javascript
const obj = {
    a: 1,
    b: 2
};

console.log(obj.hasOwnProperty('a')); // Output: true
console.log(obj.hasOwnProperty('c')); // Output: false
```

It is often used in `for...in` loops to filter out properties from the prototype chain.

**Example:**
```javascript
const obj = {
    a: 1
};

Object.prototype.b = 2; // Adding a property to the prototype chain

for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
        console.log(key); // Output: 'a' (not 'b')
    }
}
```

### 16. Discuss the advantages and disadvantages of using built-in objects compared to custom objects.

**Advantages of Built-in Objects:**

- **Standardized:** Built-in objects like `Array`, `Date`, and `Math` are standardized and well-tested.
- **Optimized:** They are optimized for performance and have built-in methods that are generally efficient.
- **Compatibility:** They provide functionality consistent across different JavaScript environments and browsers.

**Disadvantages of Built-in Objects:**

- **Limited Customization:** Built-in objects may not fit specific use cases and might not be customizable.
- **Overhead:** Some built-in objects might have more overhead than needed for simple tasks.
- **Complexity:** Using built-in objects might introduce complexity due to their extensive feature sets and behavior.

**Advantages of Custom Objects:**

- **Flexibility:** Custom objects can be tailored to fit specific requirements and functionalities.
- **Encapsulation:** You can encapsulate specific behaviors and properties relevant to your application.
- **Simplicity:** Custom objects can be simpler and more focused on particular tasks.

**Disadvantages of Custom Objects:**

- **Reinventing the Wheel:** You may end up recreating functionality that is already well-implemented in built-in objects.
- **Maintenance:** Custom objects require more maintenance and testing compared to standard built-in objects.

### 17. Can you provide an example of using the `Symbol` object to create unique identifiers in JavaScript?

The `Symbol` object is used

 to create unique and immutable identifiers that are often used as property keys.

**Example:**
```javascript
const uniqueId = Symbol('id');

const obj = {
    [uniqueId]: 123
};

console.log(obj[uniqueId]); // Output: 123

// Symbols are unique, even if created with the same description
const anotherId = Symbol('id');
console.log(uniqueId === anotherId); // Output: false
```

**Use Case:** Symbols can be used to create unique property keys, which can be useful for avoiding name collisions in objects, especially in libraries or large codebases where multiple parts of code might interact with the same objects.