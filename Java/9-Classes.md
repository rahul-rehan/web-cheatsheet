# Classes

### 1. What is a Class in Java? Explain Its Role in Object-Oriented Programming.

**Class**: 
- A class in Java is a blueprint for creating objects. It defines a data structure that contains fields (variables) and methods (functions) that operate on the data.
- In object-oriented programming (OOP), a class encapsulates data and methods that work on that data, allowing the creation of objects that model real-world entities.

**Code Snippet**:
```java
// Define a class named 'Car'
public class Car {
    // Fields (attributes)
    private String make;
    private String model;
    private int year;

    // Constructor
    public Car(String make, String model, int year) {
        this.make = make;
        this.model = model;
        this.year = year;
    }

    // Method to display car details
    public void displayInfo() {
        System.out.println("Make: " + make + ", Model: " + model + ", Year: " + year);
    }
}

// Main class to test Car
public class Main {
    public static void main(String[] args) {
        Car myCar = new Car("Toyota", "Corolla", 2020);
        myCar.displayInfo(); // Output: Make: Toyota, Model: Corolla, Year: 2020
    }
}
```

### 2. Differentiate Between a Class and an Object.

**Class**:
- A class is a blueprint or template that defines the structure and behavior (methods and fields) for objects.
- It does not occupy memory until an object is created from it.

**Object**:
- An object is an instance of a class. It represents a specific entity with actual values for the attributes defined in the class.
- Each object occupies memory and has its own state and behavior based on the class blueprint.

**Code Snippet**:
```java
public class Person {
    String name;
    int age;

    // Method to display person details
    public void displayInfo() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        // Create objects of the Person class
        Person person1 = new Person();
        person1.name = "Alice";
        person1.age = 30;
        person1.displayInfo(); // Output: Name: Alice, Age: 30

        Person person2 = new Person();
        person2.name = "Bob";
        person2.age = 25;
        person2.displayInfo(); // Output: Name: Bob, Age: 25
    }
}
```

### 3. Explain the Concept of Encapsulation. How is It Achieved in Java Classes?

**Encapsulation**:
- Encapsulation is the practice of wrapping data (fields) and methods into a single unit, known as a class. It restricts direct access to some of the object's components and is achieved using access modifiers.
- It provides control over the data by exposing only necessary methods and hiding implementation details.

**Achieved in Java**:
- By making fields private and providing public getter and setter methods to access and update field values.

**Code Snippet**:
```java
public class Employee {
    // Private fields
    private String name;
    private double salary;

    // Constructor
    public Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    // Public getter method
    public String getName() {
        return name;
    }

    // Public setter method
    public void setName(String name) {
        this.name = name;
    }

    // Public getter method
    public double getSalary() {
        return salary;
    }

    // Public setter method
    public void setSalary(double salary) {
        this.salary = salary;
    }
}

public class Main {
    public static void main(String[] args) {
        Employee emp = new Employee("John", 50000);
        System.out.println("Name: " + emp.getName() + ", Salary: " + emp.getSalary());
        emp.setSalary(55000);
        System.out.println("Updated Salary: " + emp.getSalary());
    }
}
```

### 4. What Are Access Modifiers? Explain the Difference Between Public, Private, Protected, and Default.

**Access Modifiers**:
- **Public**: The member is accessible from any other class.
- **Private**: The member is accessible only within the class it is declared.
- **Protected**: The member is accessible within the same package and by subclasses (even if they are in different packages).
- **Default** (Package-Private): The member is accessible only within the same package.

**Code Snippet**:
```java
public class AccessModifiersExample {
    public int publicField = 1; // Accessible everywhere
    private int privateField = 2; // Accessible only within this class
    protected int protectedField = 3; // Accessible within the same package and subclasses
    int defaultField = 4; // Accessible within the same package

    // Methods to demonstrate access
    public void displayAccess() {
        System.out.println("Public Field: " + publicField);
        System.out.println("Private Field: " + privateField);
        System.out.println("Protected Field: " + protectedField);
        System.out.println("Default Field: " + defaultField);
    }
}

public class TestAccess {
    public static void main(String[] args) {
        AccessModifiersExample example = new AccessModifiersExample();
        example.displayAccess();
        System.out.println("Public Field Access: " + example.publicField);
        // System.out.println("Private Field Access: " + example.privateField); // Error
        System.out.println("Protected Field Access: " + example.protectedField);
        System.out.println("Default Field Access: " + example.defaultField);
    }
}
```

### 5. What Are the Four Pillars of Object-Oriented Programming? Explain Each with Examples.

**1. Encapsulation**:
- Bundling data and methods that operate on the data into a single unit, typically a class.
- Example: Using private fields and public getters/setters.

**2. Inheritance**:
- Mechanism where a new class (subclass) inherits properties and behaviors from an existing class (superclass).
- Example: `class Dog extends Animal`.

**3. Polymorphism**:
- Ability of different classes to be treated as instances of the same class through a common interface.
- **Static Polymorphism** (Method Overloading): Same method name with different parameters.
- **Dynamic Polymorphism** (Method Overriding): Overriding methods in subclasses.

**4. Abstraction**:
- Hiding complex implementation details and showing only essential features.
- Example: Using abstract classes and interfaces.

**Code Snippet**:
```java
// Encapsulation example
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}

// Inheritance example
class Employee extends Person {
    private double salary;

    public Employee(String name, int age, double salary) {
        super(name, age);
        this.salary = salary;
    }

    public double getSalary() {
        return salary;
    }
}

// Polymorphism example
class Animal {
    public void makeSound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    public void makeSound() {
        System.out.println("Bark");
    }
}

class Cat extends Animal {
    public void makeSound() {
        System.out.println("Meow");
    }
}

// Abstraction example
abstract class Shape {
    abstract double calculateArea();
}

class Rectangle extends Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    double calculateArea() {
        return width * height;
    }
}

public class OOPExamples {
    public static void main(String[] args) {
        // Encapsulation
        Person person = new Person("John", 25);
        System.out.println("Person: " + person.getName() + ", Age: " + person.getAge());

        // Inheritance
        Employee emp = new Employee("Alice", 30, 50000);
        System.out.println("Employee: " + emp.getName() + ", Salary: " + emp.getSalary());

        // Polymorphism
        Animal animal = new Dog();
        animal.makeSound(); // Output: Bark

        // Abstraction
        Shape shape = new Rectangle(5, 10);
        System.out.println("Rectangle area: " + shape.calculateArea()); // Output: 50.0
    }
}
```

### 6. Explain the Concept of Inheritance. What Are Its Types?

**Inheritance**:
- Inheritance allows a new class (subclass) to inherit properties and methods from an existing class (superclass). It promotes code reusability and establishes a natural hierarchy.

**Types of Inheritance**:
1. **Single Inheritance**: A class inherits from one superclass.
2. **Multiple Inheritance (through interfaces)**: A class implements multiple interfaces (Java does not support multiple inheritance through classes).
3. **Multilevel Inheritance**: A class inherits from another class which is also inherited by another class.
4. **Hierarchical Inheritance**: Multiple classes inherit from the same superclass.
5. **Hybrid Inheritance**: A combination of

 multiple types of inheritance.

**Code Snippet**:
```java
// Single Inheritance
class Animal {
    void eat() {
        System.out.println("Eating...");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Barking...");
    }
}

// Multilevel Inheritance
class Grandparent {
    void heritage() {
        System.out.println("Inherited wealth...");
    }
}

class Parent extends Grandparent {
    void skills() {
        System.out.println("Inherited skills...");
    }
}

class Child extends Parent {
    void hobbies() {
        System.out.println("Inherited hobbies...");
    }
}

public class InheritanceExample {
    public static void main(String[] args) {
        // Single Inheritance
        Dog dog = new Dog();
        dog.eat();
        dog.bark();

        // Multilevel Inheritance
        Child child = new Child();
        child.heritage();
        child.skills();
        child.hobbies();
    }
}
```

### 7. What is Polymorphism? Explain Its Static and Dynamic Forms with Examples.

**Polymorphism**:
- Polymorphism allows objects to be treated as instances of their parent class rather than their actual class. It means "many shapes" and can be achieved in two forms: static (compile-time) and dynamic (run-time).

**Static Polymorphism (Method Overloading)**:
- Multiple methods with the same name but different parameters in the same class.

**Dynamic Polymorphism (Method Overriding)**:
- A subclass provides a specific implementation of a method that is already defined in its superclass.

**Code Snippet**:
```java
// Static Polymorphism (Method Overloading)
class MathOperations {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}

// Dynamic Polymorphism (Method Overriding)
class Animal {
    void makeSound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Bark");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Meow");
    }
}

public class PolymorphismExample {
    public static void main(String[] args) {
        // Static Polymorphism
        MathOperations math = new MathOperations();
        System.out.println(math.add(5, 3)); // Output: 8
        System.out.println(math.add(5.5, 3.2)); // Output: 8.7

        // Dynamic Polymorphism
        Animal myAnimal = new Dog();
        myAnimal.makeSound(); // Output: Bark

        myAnimal = new Cat();
        myAnimal.makeSound(); // Output: Meow
    }
}
```

### 8. Explain Method Overloading and Method Overriding.

**Method Overloading**:
- Method overloading occurs when two or more methods in the same class have the same name but different parameters (different type, number, or both).

**Method Overriding**:
- Method overriding happens when a subclass provides a specific implementation of a method that is already defined in its superclass with the same name and parameters.

**Code Snippet**:
```java
// Method Overloading
class Printer {
    void print(int number) {
        System.out.println("Printing number: " + number);
    }

    void print(String text) {
        System.out.println("Printing text: " + text);
    }
}

// Method Overriding
class Animal {
    void makeSound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Bark");
    }
}

public class MethodExample {
    public static void main(String[] args) {
        // Method Overloading
        Printer printer = new Printer();
        printer.print(10); // Output: Printing number: 10
        printer.print("Hello"); // Output: Printing text: Hello

        // Method Overriding
        Animal animal = new Dog();
        animal.makeSound(); // Output: Bark
    }
}
```

### 9. What is the Difference Between Early and Late Binding?

**Early Binding**:
- Also known as static binding, it occurs at compile time. Method calls are resolved to their corresponding methods during the compile time.
- Example: Method overloading (where the method is selected based on the compile-time type of the arguments).

**Late Binding**:
- Also known as dynamic binding, it occurs at runtime. The method call is resolved to the appropriate method based on the object's runtime type.
- Example: Method overriding (where the method to be called is determined based on the object's runtime type).

**Code Snippet**:
```java
// Early Binding (Static Binding)
class Printer {
    void print(int number) {
        System.out.println("Printing number: " + number);
    }

    void print(String text) {
        System.out.println("Printing text: " + text);
    }
}

// Late Binding (Dynamic Binding)
class Animal {
    void makeSound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("Bark");
    }
}

public class BindingExample {
    public static void main(String[] args) {
        // Early Binding
        Printer printer = new Printer();
        printer.print(10); // Output: Printing number: 10
        printer.print("Hello"); // Output: Printing text: Hello

        // Late Binding
        Animal animal = new Dog(); // Reference type: Animal, Object type: Dog
        animal.makeSound(); // Output: Bark (method overridden in Dog)
    }
}
```

### 10. Explain the Use of Constructors and Destructors in Java.

**Constructors**:
- Constructors are special methods used to initialize objects. They have the same name as the class and no return type.
- A constructor is invoked when an object is created and sets up initial state or performs startup operations.

**Destructors**:
- Java does not have explicit destructors. Instead, Java relies on garbage collection to clean up unused objects.
- The `finalize()` method is provided in `Object` class, which is called by the garbage collector before an object is destroyed, but it's not commonly used.

**Code Snippet**:
```java
class Car {
    private String model;

    // Constructor
    public Car(String model) {
        this.model = model;
        System.out.println("Car model: " + model);
    }

    // Destructor-like behavior (not a real destructor)
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Car object is being collected.");
        super.finalize();
    }
}

public class ConstructorDestructorExample {
    public static void main(String[] args) {
        Car myCar = new Car("Toyota");
        // Explicitly suggest garbage collection (not recommended in practice)
        myCar = null;
        System.gc(); // Request garbage collection
    }
}
```

### 11. What is the Difference Between a Class and an Interface?

**Class**:
- A class is a blueprint for creating objects and can contain fields, methods, constructors, and nested classes.
- Classes support inheritance, meaning one class can extend another class.

**Interface**:
- An interface is a reference type that can contain only method signatures (abstract methods), default methods, static methods, and constants.
- Interfaces are used to define a contract that other classes must adhere to, supporting multiple inheritance through interfaces.

**Code Snippet**:
```java
// Class
class Car {
    private String model;

    public Car(String model) {
        this.model = model;
    }

    public void displayModel() {
        System.out.println("Car model: " + model);
    }
}

// Interface
interface Vehicle {
    void start(); // Abstract method

    default void honk() { // Default method
        System.out.println("Honking...");
    }
}

// Implementing Interface
class Bike implements Vehicle {
    @Override
    public void start() {
        System.out.println("Bike started.");
    }
}

public class ClassInterfaceExample {
    public static void main(String[] args) {
        Car car = new Car("Honda");
        car.displayModel();

        Bike bike = new Bike();
        bike.start(); // Output: Bike started.
        bike.honk();  // Output: Honking...
    }
}
```

### 12. Explain the Concept of Abstract Classes. When Would You Use an Abstract Class Over an Interface?

**Abstract Class**:
- An abstract class cannot be instantiated and may contain abstract methods (methods without a body) and concrete methods (methods with a body).
- It is used to provide a common base class with shared functionality for other classes to extend.

**When to Use Abstract Class Over Interface**:
- Use an abstract class when you want to share code among several closely related classes.
- Use an interface when you need to specify a common behavior that can be implemented by classes from different hierarchies.

**Code Snippet**:
```java
abstract class Shape {
    abstract double calculateArea(); // Abstract method

    public void display() { // Concrete method
        System.out.println("Displaying shape.");
    }
}

class Rectangle extends Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    double calculateArea() {
        return width * height;
    }
}

public class AbstractClassExample {
    public static void main(String[] args) {
        Shape shape = new Rectangle(5, 10);
        shape.display(); // Output: Displaying shape.
        System.out.println("Area: " + shape.calculateArea()); // Output: Area: 50.0
    }
}
```

### 13. What is the Difference Between `final`, `finally`, and `finalize`?

**`final`**:
- Used to declare constants, prevent method overriding, and inheritance of classes.
- `final` variables cannot be reassigned, `final` methods cannot be overridden, and `final` classes cannot be subclassed.

**`finally`**:
- A block that follows a `try-catch` block. It always executes, regardless of whether an exception was thrown or not.
- Used for cleanup code like closing files or releasing resources.

**`finalize()`**:
- A method in the `Object` class that is called by the garbage collector before an object is destroyed.
- It is not commonly used and its use is generally discouraged due to its non-deterministic nature.

**Code Snippet**:
```java
// final keyword
final class ImmutableClass {
    final int value = 100; // Constant value

    final void display() {
        System.out.println("Value: " + value);
    }
}

// finally block
class FinallyExample {
    public static void main(String[] args) {
        try {
            System.out.println("Inside try block.");
            int result = 10 / 0; // Exception
        } catch (ArithmeticException e) {
            System.out.println("Caught exception: " + e);
        } finally {
            System.out.println("This block always executes.");
        }
    }
}

// finalize() method
class Resource {
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Resource is being finalized.");
        super.finalize();
    }
}

public class FinalizeExample {
    public static void main(String[] args) {
        Resource res = new Resource();
        res = null; // Suggest garbage collection
        System.gc(); // Request garbage collection
    }
}
```

### 14. Explain the Concept of Static Variables and Methods. When Would You Use Them?

**Static Variables**:
- Belong to the class, rather than instances of the class. They are shared among all instances.
- Useful for constants or variables that need to be common to all instances.

**Static Methods**:
- Belong to the class and can be called without creating an instance of the class.
- Useful for utility or helper methods that don't require object state.

**Code Snippet**:
```java
class MathUtility {
    static final double PI = 3.14159; // Static variable

    static double square(double number) { // Static method
        return number * number;
    }
}

public class StaticExample {
    public static void main(String[] args) {
        System.out.println("PI: " + MathUtility.PI); // Access static variable
        System.out.println("Square of 5: " + MathUtility.square(5)); // Call static method
    }
}
```

### 15. What is the Difference Between Instance and Class Variables?

**Instance Variables**:
- Declared inside a class but outside any method, constructor, or block.
- Each instance of the class has its own copy of the instance variables.

**Class Variables**:
- Declared with the `static` keyword.
- Shared among all instances of the class. Only one copy of a class variable exists, regardless of the number of objects.

**Code Snippet**:
```java
class Example {
    int instanceVar = 0; // Instance variable
    static int classVar = 0; // Class variable

    void increment() {
        instanceVar++;
        classVar++;
    }
}

public class VariableExample {
    public static void main(String[] args) {
        Example obj1 = new Example();
        Example obj2 = new Example();

        obj1.increment();
        System.out.println("obj1 instanceVar: " + obj1.instanceVar); // Output: 1
        System.out.println("obj1 classVar: " + obj1.classVar); // Output: 1
        System.out.println("obj2 instanceVar: " + obj2.instanceVar); // Output: 0
        System.out.println

("obj2 classVar: " + obj2.classVar); // Output: 1
    }
}
```

### 16. Explain the Concept of Inner Classes. What Are the Different Types of Inner Classes?

**Inner Classes**:
- Classes defined within another class. They can access the members of the enclosing class, including private members.

**Types of Inner Classes**:
1. **Non-Static Nested Classes (Inner Classes)**: Associated with an instance of the outer class.
2. **Static Nested Classes**: Associated with the outer class itself and do not have access to instance variables of the outer class.
3. **Local Classes**: Defined within a method or block and are scoped to that block.
4. **Anonymous Classes**: Used to instantiate objects with certain modifications or overrides without naming the class.

**Code Snippet**:
```java
class Outer {
    private String outerField = "Outer Field";

    // Non-static nested class (Inner Class)
    class Inner {
        void display() {
            System.out.println("Accessing from Inner class: " + outerField);
        }
    }

    // Static nested class
    static class StaticNested {
        void display() {
            System.out.println("Static Nested class");
        }
    }

    void method() {
        // Local class
        class Local {
            void display() {
                System.out.println("Local class inside method");
            }
        }
        Local local = new Local();
        local.display();
    }
}

public class InnerClassExample {
    public static void main(String[] args) {
        // Non-static inner class
        Outer outer = new Outer();
        Outer.Inner inner = outer.new Inner();
        inner.display(); // Output: Accessing from Inner class: Outer Field

        // Static nested class
        Outer.StaticNested staticNested = new Outer.StaticNested();
        staticNested.display(); // Output: Static Nested class

        // Local class
        Outer outerObj = new Outer();
        outerObj.method(); // Output: Local class inside method
    }
}
```

### 17. How is Memory Allocated for Objects in Java? Explain the Heap and Stack Memory.

**Memory Allocation in Java**:

1. **Stack Memory**:
   - **Purpose**: Stores method calls, local variables, and control flow information.
   - **Characteristics**: Memory allocation is fast and automatically managed. The stack is organized in a last-in-first-out (LIFO) manner.
   - **Scope**: Each thread has its own stack. Variables in the stack are local to the thread and are automatically deallocated when the method call completes.

2. **Heap Memory**:
   - **Purpose**: Stores objects and their instance variables. It is used for dynamic memory allocation.
   - **Characteristics**: Managed by the garbage collector. Objects are created using the `new` keyword, and their memory is reclaimed when they are no longer referenced.
   - **Scope**: Shared among all threads in a Java application. The heap is larger and slower compared to the stack but is essential for object management.

**Code Snippet**:
```java
public class MemoryExample {
    int instanceVar; // This is stored in the heap (part of object state)

    void method() {
        int localVar = 10; // This is stored in the stack (local to method)
        MemoryExample obj = new MemoryExample(); // Object is stored in the heap
    }
}
```

### 18. Explain Garbage Collection in Java.

**Garbage Collection**:
- **Purpose**: Automatically reclaims memory occupied by objects that are no longer referenced in the program.
- **Process**:
  1. **Marking**: Identifies which objects are still referenced and which are not.
  2. **Normal Deletion**: Removes unreferenced objects.
  3. **Deletion with Compaction**: Reclaims space and may move objects to reduce fragmentation.
- **Types**:
  - **Minor GC**: Reclaims space from the Young Generation.
  - **Major GC**: Reclaims space from the Old Generation.

**Code Snippet**:
```java
public class GarbageCollectionExample {
    public static void main(String[] args) {
        GarbageCollectionExample obj1 = new GarbageCollectionExample();
        GarbageCollectionExample obj2 = new GarbageCollectionExample();

        obj1 = null; // Object is no longer referenced
        System.gc(); // Suggest garbage collection
    }

    @Override
    protected void finalize() throws Throwable {
        System.out.println("Object is being collected.");
        super.finalize();
    }
}
```

### 19. What is the Difference Between a Shallow Copy and a Deep Copy?

**Shallow Copy**:
- **Definition**: Creates a new object, but copies only the references to the objects, not the actual objects themselves. Thus, both the original and the copied object refer to the same nested objects.
- **Method**: `clone()` method with default implementation or using `Object.clone()`.

**Deep Copy**:
- **Definition**: Creates a new object and recursively copies all objects referenced by the original object, resulting in a completely independent copy.
- **Method**: Manually implementing deep copy or using serialization.

**Code Snippet**:
```java
import java.util.ArrayList;
import java.util.List;

class Person implements Cloneable {
    String name;
    List<String> hobbies;

    Person(String name, List<String> hobbies) {
        this.name = name;
        this.hobbies = hobbies;
    }

    // Shallow Copy
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    // Deep Copy
    public Person deepClone() {
        List<String> newHobbies = new ArrayList<>(this.hobbies);
        return new Person(this.name, newHobbies);
    }
}

public class CopyExample {
    public static void main(String[] args) throws CloneNotSupportedException {
        List<String> hobbies = new ArrayList<>();
        hobbies.add("Reading");
        Person original = new Person("John", hobbies);

        // Shallow copy
        Person shallowCopy = (Person) original.clone();
        shallowCopy.hobbies.add("Swimming");
        System.out.println(original.hobbies); // Output: [Reading, Swimming]

        // Deep copy
        Person deepCopy = original.deepClone();
        deepCopy.hobbies.add("Cycling");
        System.out.println(original.hobbies); // Output: [Reading, Swimming]
        System.out.println(deepCopy.hobbies); // Output: [Reading, Cycling]
    }
}
```

### 20. How Do You Achieve Code Reusability in Java?

**Code Reusability**:
- **Inheritance**: Allows classes to inherit fields and methods from another class, promoting reuse.
- **Composition**: Uses objects of other classes within a class, reusing their functionality.
- **Interfaces**: Define methods that can be implemented by multiple classes, providing a common functionality.

**Code Snippet**:
```java
// Inheritance
class Vehicle {
    void start() {
        System.out.println("Vehicle started");
    }
}

class Car extends Vehicle {
    void honk() {
        System.out.println("Car honks");
    }
}

public class ReusabilityExample {
    public static void main(String[] args) {
        Car car = new Car();
        car.start(); // Reused method from Vehicle
        car.honk();  // Car-specific method
    }
}
```

### 21. Design a Class to Represent a Car. Include Attributes like Make, Model, Year, and Methods like Start, Stop, Accelerate.

**Code Snippet**:
```java
class Car {
    private String make;
    private String model;
    private int year;

    public Car(String make, String model, int year) {
        this.make = make;
        this.model = model;
        this.year = year;
    }

    public void start() {
        System.out.println("The car is starting");
    }

    public void stop() {
        System.out.println("The car is stopping");
    }

    public void accelerate() {
        System.out.println("The car is accelerating");
    }

    @Override
    public String toString() {
        return year + " " + make + " " + model;
    }
}

public class CarExample {
    public static void main(String[] args) {
        Car car = new Car("Toyota", "Corolla", 2022);
        System.out.println(car);
        car.start();
        car.accelerate();
        car.stop();
    }
}
```

### 22. Create a Class Hierarchy for Animals with Base Class Animal and Derived Classes like Dog, Cat, and Bird.

**Code Snippet**:
```java
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }

    void sleep() {
        System.out.println("This animal sleeps.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

class Cat extends Animal {
    void meow() {
        System.out.println("The cat meows.");
    }
}

class Bird extends Animal {
    void fly() {
        System.out.println("The bird flies.");
    }
}

public class AnimalHierarchy {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();
        dog.bark();
        dog.sleep();

        Cat cat = new Cat();
        cat.meow();
        cat.eat();
        cat.sleep();

        Bird bird = new Bird();
        bird.fly();
        bird.eat();
        bird.sleep();
    }
}
```

### 23. Explain How You Would Design a Class for a Banking System.

**Design**:
1. **Classes**:
   - **Account**: Base class with common attributes and methods.
   - **SavingsAccount** and **CheckingAccount**: Derived classes with specific functionalities.

2. **Attributes**:
   - Account number, account holder, balance.

3. **Methods**:
   - Deposit, withdraw, check balance, transfer funds.

**Code Snippet**:
```java
abstract class Account {
    protected String accountNumber;
    protected double balance;

    public Account(String accountNumber) {
        this.accountNumber = accountNumber;
        this.balance = 0.0;
    }

    public void deposit(double amount) {
        balance += amount;
    }

    public void withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
        } else {
            System.out.println("Insufficient funds.");
        }
    }

    public double getBalance() {
        return balance;
    }

    @Override
    public String toString() {
        return "Account Number: " + accountNumber + ", Balance: " + balance;
    }
}

class SavingsAccount extends Account {
    private double interestRate;

    public SavingsAccount(String accountNumber, double interestRate) {
        super(accountNumber);
        this.interestRate = interestRate;
    }

    public void applyInterest() {
        balance += balance * interestRate;
    }
}

class CheckingAccount extends Account {
    private double overdraftLimit;

    public CheckingAccount(String accountNumber, double overdraftLimit) {
        super(accountNumber);
        this.overdraftLimit = overdraftLimit;
    }

    @Override
    public void withdraw(double amount) {
        if (amount <= balance + overdraftLimit) {
            balance -= amount;
        } else {
            System.out.println("Overdraft limit exceeded.");
        }
    }
}

public class BankingSystem {
    public static void main(String[] args) {
        SavingsAccount savings = new SavingsAccount("123456", 0.03);
        savings.deposit(1000);
        savings.applyInterest();
        System.out.println(savings);

        CheckingAccount checking = new

 CheckingAccount("654321", 500);
        checking.deposit(500);
        checking.withdraw(600);
        System.out.println(checking);
    }
}
```

### 24. How Would You Implement a Singleton Pattern in Java?

**Singleton Pattern** ensures that a class has only one instance and provides a global point of access to it.

**Code Snippet**:
```java
public class Singleton {
    private static Singleton instance;

    // Private constructor to prevent instantiation
    private Singleton() { }

    // Method to get the single instance of the class
    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

public class SingletonTest {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();

        System.out.println(s1 == s2); // Output: true
    }
}
```

### 25. Explain the Use of Design Patterns in Class Design.

**Design Patterns** are typical solutions to common problems in software design. They provide a way to reuse successful designs and architectures. Some benefits include:
- **Improved Code Reusability**: Patterns provide well-tested solutions that can be reused.
- **Ease of Maintenance**: They make code easier to understand and modify.
- **Standardization**: They provide a standard terminology and design approach.

**Examples**:
- **Singleton**: Ensures a class has only one instance.
- **Factory Method**: Creates objects without specifying the exact class to instantiate.
- **Observer**: Defines a dependency between objects so that when one object changes state, all its dependents are notified.

### 26. What is the Difference Between a Class Loader and a JVM?

**Class Loader**:
- **Purpose**: Responsible for loading classes into the JVM at runtime.
- **Functionality**: It reads the `.class` files and loads them into the JVM memory.

**JVM (Java Virtual Machine)**:
- **Purpose**: Executes Java bytecode.
- **Functionality**: Provides runtime environment, manages memory, and performs garbage collection.

**Code Snippet** (for understanding ClassLoader):
```java
public class ClassLoaderExample {
    public static void main(String[] args) {
        ClassLoader classLoader = ClassLoaderExample.class.getClassLoader();
        System.out.println("Class Loader: " + classLoader);
    }
}
```

### 27. Explain the Concept of Reflection in Java.

**Reflection** allows a Java program to inspect and manipulate classes, methods, and fields at runtime, even if they are private.

**Code Snippet**:
```java
import java.lang.reflect.Method;

public class ReflectionExample {
    public static void main(String[] args) throws Exception {
        Class<?> clazz = Class.forName("java.util.ArrayList");
        Method[] methods = clazz.getDeclaredMethods();

        for (Method method : methods) {
            System.out.println(method.getName());
        }
    }
}
```

### 28. How Do You Achieve Serialization in Java?

**Serialization** allows an object to be converted into a byte stream and later reconstructed.

**Steps**:
1. Implement `Serializable` interface.
2. Use `ObjectOutputStream` to serialize.
3. Use `ObjectInputStream` to deserialize.

**Code Snippet**:
```java
import java.io.*;

class Person implements Serializable {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}

public class SerializationExample {
    public static void main(String[] args) {
        Person person = new Person("John Doe", 30);

        // Serialize
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("person.ser"))) {
            oos.writeObject(person);
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Deserialize
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("person.ser"))) {
            Person deserializedPerson = (Person) ois.readObject();
            System.out.println(deserializedPerson);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

### 29. What is the Difference Between a Checked and Unchecked Exception?

**Checked Exceptions**:
- **Definition**: Exceptions that are checked at compile-time.
- **Requirement**: Must be either caught or declared in the method signature using `throws`.
- **Example**: `IOException`, `SQLException`.

**Unchecked Exceptions**:
- **Definition**: Exceptions that are not checked at compile-time.
- **Requirement**: Not required to be caught or declared.
- **Example**: `NullPointerException`, `ArrayIndexOutOfBoundsException`.

**Code Snippet**:
```java
public class ExceptionExample {
    public static void main(String[] args) {
        // Checked Exception
        try {
            FileReader file = new FileReader("file.txt");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Unchecked Exception
        try {
            int[] arr = new int[5];
            arr[10] = 1; // ArrayIndexOutOfBoundsException
        } catch (ArrayIndexOutOfBoundsException e) {
            e.printStackTrace();
        }
    }
}
```

### 30. Explain the Use of Generics in Java.

**Generics** provide a way to define classes, interfaces, and methods with a placeholder for types. They enable type safety and eliminate the need for casting.

**Benefits**:
- **Type Safety**: Ensures type correctness at compile-time.
- **Eliminates Casts**: Reduces the need for explicit casting.

**Code Snippet**:
```java
import java.util.ArrayList;
import java.util.List;

class GenericBox<T> {
    private T value;

    public void setValue(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}

public class GenericsExample {
    public static void main(String[] args) {
        GenericBox<String> stringBox = new GenericBox<>();
        stringBox.setValue("Hello, Generics!");
        System.out.println(stringBox.getValue()); // Output: Hello, Generics!

        GenericBox<Integer> intBox = new GenericBox<>();
        intBox.setValue(123);
        System.out.println(intBox.getValue()); // Output: 123
    }
}
```