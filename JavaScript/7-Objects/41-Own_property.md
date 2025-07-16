## 1. What is meant by "own property" of an object in JavaScript?

An **own property** is a property that is directly defined on the object itself, not inherited through the prototype chain.

## 2. How are own properties different from inherited properties?

- **Own properties** exist directly on the object instance.
- **Inherited properties** come from the object's prototype or further up the prototype chain.
- Own properties belong specifically to the object, whereas inherited properties are shared through prototypal inheritance.

## 3. How can you check if a property is an own property of an object?

You can use the method `hasOwnProperty()` to check if a property is an own property.

#### Example:
```javascript
const proto = { inheritedProp: 1 };
const obj = Object.create(proto);
obj.ownProp = 2;

console.log(obj.hasOwnProperty("ownProp"));       // true
console.log(obj.hasOwnProperty("inheritedProp")); // false
```
## 4. What does the `hasOwnProperty()` method do?

The `hasOwnProperty()` method checks whether an object has a specific property as its **own property** (i.e., not inherited through the prototype chain).  
It returns `true` if the property exists directly on the object, and `false` otherwise.

## 5. What is the difference between `in` operator and `hasOwnProperty()`?

| Aspect                     | `in` Operator                                  | `hasOwnProperty()`                               |
|----------------------------|-----------------------------------------------|-------------------------------------------------|
| Checks own or inherited?    | Checks **both own and inherited** properties  | Checks **only own** properties                   |
| Usage                      | `'propertyName' in object`                      | `object.hasOwnProperty('propertyName')`          |
| Returns                    | `true` if property exists anywhere in the prototype chain | `true` only if property exists directly on the object |
| Example                   |```javascript<br>const obj = {a: 1};<br>console.log('a' in obj); // true<br>console.log('toString' in obj); // true (inherited)<br>``` |```javascript<br>const obj = {a: 1};<br>console.log(obj.hasOwnProperty('a')); // true<br>console.log(obj.hasOwnProperty('toString')); // false (inherited)<br>``` |

Use `hasOwnProperty()` when you want to confirm that the property belongs **directly** to the object, avoiding inherited properties.
## 6. Do own properties include non-enumerable or symbol properties?

Yes, **own properties include all properties directly defined on the object**, regardless of whether they are:

- **Enumerable or non-enumerable**
- **String-keyed or symbol-keyed**

Own properties are simply those that exist directly on the object, no matter their enumerability or key type.

## 7. Are properties defined directly in the constructor considered own properties?

Yes, properties that are **defined directly inside a constructor function on `this`** are own properties of the created object instance.

#### Example:
```javascript
function Person(name) {
  this.name = name; // own property
}

const p = new Person("Alice");
console.log(p.hasOwnProperty("name")); // true
```