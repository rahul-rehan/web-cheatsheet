# OOPs

### 1. What is Object-Oriented Programming (OOP)? Explain its Core Concepts with Real-World Examples.

**Object-Oriented Programming (OOP)** is a programming paradigm based on the concept of "objects," which can contain data and methods to manipulate that data. It promotes organizing code into reusable and modular components. The core concepts of OOP are:

- **Encapsulation**: Bundling data (fields) and methods (functions) into a single unit, called a class. Example: A `Car` class with fields like `color` and `speed` and methods like `accelerate()` and `brake()`.

- **Inheritance**: Mechanism by which one class (subclass) inherits fields and methods from another class (superclass). Example: A `SportsCar` class inherits from the `Car` class, gaining its features and adding more.

- **Polymorphism**: Ability of different classes to be treated as instances of the same class through a common interface. Example: The `accelerate()` method can behave differently in `Car` and `SportsCar` classes.

- **Abstraction**: Hiding the complex implementation details and showing only the necessary features of an object. Example: A `Vehicle` interface with abstract methods like `start()` and `stop()` which concrete classes like `Car` and `Bike` must implement.

**Code Snippet**:
```java
// Encapsulation
class Car {
    private String color;
    private int speed;

    public void setColor(String color) {
        this.color = color;
    }

    public String getColor() {
        return color;
    }

    public void accelerate() {
        speed += 10;
    }

    public void brake() {
        speed -= 10;
    }
}

// Inheritance
class SportsCar extends Car {
    private boolean turboBoost;

    public void setTurboBoost(boolean turboBoost) {
        this.turboBoost = turboBoost;
    }

    public void useTurboBoost() {
        if (turboBoost) {
            accelerate(); // Polymorphism
            accelerate(); // Turbo boost effect
        }
    }
}

// Polymorphism and Abstraction
interface Vehicle {
    void start();
    void stop();
}

class Bike implements Vehicle {
    public void start() {
        System.out.println("Bike starting...");
    }

    public void stop() {
        System.out.println("Bike stopping...");
    }
}

public class OOPExample {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.setColor("Red");
        System.out.println("Car color: " + myCar.getColor());

        SportsCar mySportsCar = new SportsCar();
        mySportsCar.setTurboBoost(true);
        mySportsCar.useTurboBoost();

        Vehicle myBike = new Bike();
        myBike.start();
        myBike.stop();
    }
}
```

### 2. Differentiate Between Class and Object

- **Class**: A blueprint or template for creating objects. It defines the properties (fields) and behaviors (methods) that the objects created from the class will have.
  
- **Object**: An instance of a class. It represents a concrete realization of the class with specific values for the properties defined by the class.

**Code Snippet**:
```java
// Class definition
class Person {
    String name;
    int age;

    void introduce() {
        System.out.println("Hi, I'm " + name + " and I'm " + age + " years old.");
    }
}

// Creating objects
public class ClassObjectExample {
    public static void main(String[] args) {
        Person person1 = new Person(); // Object creation
        person1.name = "Alice";
        person1.age = 30;
        person1.introduce();

        Person person2 = new Person(); // Another object
        person2.name = "Bob";
        person2.age = 25;
        person2.introduce();
    }
}
```

### 3. Explain Encapsulation, Inheritance, Polymorphism, and Abstraction with Examples

**Encapsulation**:
Encapsulation hides the internal state and requires all interaction to be performed through an object's methods.

**Code Snippet**:
```java
class Employee {
    private String name;
    private double salary;

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    public double getSalary() {
        return salary;
    }
}
```

**Inheritance**:
Inheritance allows a class to inherit fields and methods from another class.

**Code Snippet**:
```java
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks.");
    }
}
```

**Polymorphism**:
Polymorphism enables one method to perform different functions based on the object it is acting upon.

**Code Snippet**:
```java
class Shape {
    void draw() {
        System.out.println("Drawing a shape.");
    }
}

class Circle extends Shape {
    void draw() {
        System.out.println("Drawing a circle.");
    }
}

public class PolymorphismExample {
    public static void main(String[] args) {
        Shape shape = new Circle();
        shape.draw(); // Outputs: Drawing a circle.
    }
}
```

**Abstraction**:
Abstraction hides complex implementation details and shows only the necessary features.

**Code Snippet**:
```java
abstract class Animal {
    abstract void makeSound();

    void sleep() {
        System.out.println("This animal is sleeping.");
    }
}

class Cat extends Animal {
    void makeSound() {
        System.out.println("Meow");
    }
}
```

### 4. Difference Between Method Overloading and Method Overriding

- **Method Overloading**:
  - Same method name but different parameter lists (different type or number of parameters).
  - Occurs within the same class.
  - Compile-time polymorphism.

- **Method Overriding**:
  - Same method name and parameter list as the superclass method.
  - Occurs in a subclass.
  - Runtime polymorphism.

**Code Snippet**:
```java
// Method Overloading
class MathOperation {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
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
        MathOperation math = new MathOperation();
        System.out.println(math.add(5, 10)); // Overloaded method
        System.out.println(math.add(5.5, 10.5)); // Overloaded method

        Animal myAnimal = new Dog();
        myAnimal.makeSound(); // Overridden method
    }
}
```

### 5. Explain Early and Late Binding

- **Early Binding**:
  - Also known as static binding or compile-time binding.
  - The method or property to be called is resolved at compile time.
  - Applies to method overloading.

- **Late Binding**:
  - Also known as dynamic binding or runtime binding.
  - The method or property to be called is resolved at runtime.
  - Applies to method overriding.

**Code Snippet**:
```java
// Early Binding (Compile-time)
class EarlyBindingExample {
    void display(int a) {
        System.out.println("Integer: " + a);
    }

    void display(String a) {
        System.out.println("String: " + a);
    }
}

// Late Binding (Runtime)
class Animal {
    void makeSound() {
        System.out.println("Animal sound");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("Meow");
    }
}

public class BindingExample {
    public static void main(String[] args) {
        EarlyBindingExample eb = new EarlyBindingExample();
        eb.display(5); // Early binding
        eb.display("Hello"); // Early binding

        Animal myAnimal = new Cat();
        myAnimal.makeSound(); // Late binding
    }
}
```

### 6. Difference Between Interface and Abstract Class

- **Interface**:
  - Can only contain abstract methods (prior to Java 8; from Java 8 onward, it can contain default and static methods).
  - All methods are implicitly `public` and `abstract`.
  - A class can implement multiple interfaces.

- **Abstract Class**:
  - Can contain both abstract (without implementation) and concrete (with implementation) methods.
  - Can have fields, constructors, and methods with any access modifiers.
  - A class can extend only one abstract class.

**Code Snippet**:
```java
// Interface
interface Vehicle {
    void start();
    void stop();
}

// Abstract Class
abstract class Machine {
    abstract void operate();

    void turnOff() {
        System.out.println("Machine is turning off.");
    }
}

// Implementation
class Car extends Machine implements Vehicle {
    @Override
    void operate() {
        System.out.println("Car is operating.");
    }

    @Override
    public void start() {
        System.out.println("Car started.");
    }

    @Override
    public void stop() {
        System.out.println("Car stopped.");
    }
}
```

### 7. Can You Have a Private Constructor? If Yes, Why Would You Use It?

Yes, you can have a private constructor. It is often used in the Singleton Design Pattern, where only one instance of a class should be created.

**Code Snippet**:
```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // Private constructor
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

### 8. Explain the Concept of Access Modifiers (public, private, protected, default)

- **`public`**: The member is accessible from any other class.
- **`private`**: The member is accessible only within its own class.
- **`protected`**: The member is accessible within its own package and by subclasses.
- **default**: No modifier is used; the member is accessible only within its own package.

**Code Snippet**:
```java
public class AccessModifiers {
    public int publicField = 1;
    private int privateField = 2;
    protected int protectedField = 3;
    int defaultField = 4; // Default access

    public void display() {
        System.out.println("Public: " + publicField);
        System.out.println("Private: " + privateField);
        System.out.println("Protected: " + protectedField);
        System.out.println("Default: " + defaultField);
    }
}
```

### 9. Difference Between `final`, `finally`, and `finalize`

- **`final`**:
  - Can be used with variables, methods, and classes.
  - `final` variable: Cannot be changed once initialized.
  - `final` method: Cannot be overridden by subclasses.
  - `final` class: Cannot be subclassed.

- **`finally`**:
  - A block used in exception handling to execute code after a `try` block, regardless of whether an exception was thrown.

- **`finalize`**:
  - A method in the `Object` class called by the garbage collector before an object is reclaimed. It allows cleanup operations before the object is removed from memory.

**Code Snippet**:
```java
public class FinalExample {
    public final int constantValue = 10;

    public final void display() {
        System.out.println("Final method");
    }
}

class Subclass extends FinalExample {
    // Cannot override final method
    // void display() {
    //    System.out.println("Overridden method");
    // }
}

public class FinalizeExample {
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Object is being garbage collected");
        super.finalize();
    }

    public static void main(String[] args) {
        FinalizeExample obj = new FinalizeExample();
        obj = null;
        System.gc(); // Request garbage collection
    }
}
```

### 10. Explain the Concept of Garbage Collection in Java

**Garbage Collection** in Java is an automatic process of deallocating memory used by objects that are no longer referenced in a program. The Java Virtual Machine (JVM) performs garbage collection to reclaim memory and reduce the risk of memory leaks, thus improving performance and efficiency.

**Key Points:**
- The garbage collector (GC) runs in the background and is responsible for removing unused objects.
- Java provides several garbage collection algorithms, including generational and concurrent collectors.

**Code Snippet**:
```java
public class GarbageCollectionExample {
    public static void main(String[] args) {
        // Creating objects
        GarbageCollectionExample obj1 = new GarbageCollectionExample();
        GarbageCollectionExample obj2 = new GarbageCollectionExample();
        
        // Nullifying references
        obj1 = null;  // The object previously referenced by obj1 is now eligible for GC
        obj2 = null;  // The object previously referenced by obj2 is now eligible for GC
        
        // Requesting JVM to perform garbage collection
        System.gc();  // It is not guaranteed that GC will run immediately

        // Adding a custom finalize method to see when an object is collected
        System.out.println("Garbage Collection Requested.");
    }

    @Override
    protected void finalize() throws Throwable {
        System.out.println("Object is being collected by GC.");
        super.finalize();
    }
}
```

### 11. What is the Difference Between `instanceof` and Typecasting?

- **`instanceof`**: Checks whether an object is an instance of a specific class or subclass. It returns `true` or `false` and is used to ensure safe typecasting.

- **Typecasting**: Converts an object of one type to another type. It requires that the object actually be of the target type, otherwise, it throws a `ClassCastException`.

**Code Snippet**:
```java
class Animal {}
class Dog extends Animal {}

public class InstanceofTypecastingExample {
    public static void main(String[] args) {
        Animal animal = new Dog();
        
        // Using instanceof
        if (animal instanceof Dog) {
            Dog dog = (Dog) animal; // Safe typecasting
            System.out.println("Animal is a Dog");
        }
        
        // Using incorrect typecasting
        try {
            String str = (String) animal; // This will throw ClassCastException
        } catch (ClassCastException e) {
            System.out.println("Invalid typecasting: " + e.getMessage());
        }
    }
}
```

### 12. Explain the Use of `super` Keyword

The `super` keyword in Java is used to refer to the immediate parent class of the current object. It is used to:
- Call the parent class's constructor.
- Access parent class methods that have been overridden in the child class.
- Access parent class fields.

**Code Snippet**:
```java
class Animal {
    String name = "Animal";

    Animal() {
        System.out.println("Animal Constructor");
    }

    void display() {
        System.out.println("Animal display");
    }
}

class Dog extends Animal {
    String name = "Dog";

    Dog() {
        super(); // Calls the Animal constructor
        System.out.println("Dog Constructor");
    }

    void display() {
        super.display(); // Calls the Animal display method
        System.out.println("Dog display");
    }

    void showNames() {
        System.out.println("Dog's name: " + name); // Refers to Dog's name
        System.out.println("Animal's name: " + super.name); // Refers to Animal's name
    }
}

public class SuperKeywordExample {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.display();
        dog.showNames();
    }
}
```

### 13. What is the Difference Between `this` and `super` Keywords?

- **`this`**: Refers to the current instance of the class. It is used to:
  - Access instance variables and methods.
  - Invoke the current class's constructor.
  - Resolve naming conflicts between instance variables and parameters.

- **`super`**: Refers to the superclass of the current instance. It is used to:
  - Access superclass methods and variables.
  - Call superclass constructors.

**Code Snippet**:
```java
class Parent {
    void show() {
        System.out.println("Parent show");
    }
}

class Child extends Parent {
    void show() {
        super.show(); // Calls Parent's show method
        System.out.println("Child show");
    }

    void display() {
        this.show(); // Calls Child's show method
    }
}

public class ThisSuperKeywordExample {
    public static void main(String[] args) {
        Child child = new Child();
        child.display(); // Outputs: Parent show \n Child show
    }
}
```

### 14. What is the Difference Between `new` and `clone`?

- **`new`**: Creates a new instance of a class by calling its constructor. It allocates memory for a new object and initializes it.

- **`clone`**: Creates a copy of an existing object. It is used for creating a shallow copy of an object that implements the `Cloneable` interface.

**Code Snippet**:
```java
class Person implements Cloneable {
    String name;

    Person(String name) {
        this.name = name;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // Shallow copy
    }
}

public class NewVsCloneExample {
    public static void main(String[] args) {
        Person person1 = new Person("Alice");
        try {
            Person person2 = (Person) person1.clone(); // Cloning person1
            System.out.println("Original: " + person1.name);
            System.out.println("Clone: " + person2.name);
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}
```

### 15. Explain the Concept of Inner Classes

**Inner Classes** are classes defined within another class. They can access the members of the outer class and can be categorized as:
- **Member Inner Class**: Non-static inner class.
- **Static Nested Class**: Static inner class.
- **Local Inner Class**: Defined inside a method.
- **Anonymous Inner Class**: Without a name, used for implementing interfaces or extending classes.

**Code Snippet**:
```java
class OuterClass {
    private String outerField = "Outer";

    class InnerClass {
        void display() {
            System.out.println("Inner class accessing: " + outerField);
        }
    }

    static class StaticNestedClass {
        void show() {
            System.out.println("Static nested class");
        }
    }

    void method() {
        class LocalInnerClass {
            void print() {
                System.out.println("Local inner class");
            }
        }
        LocalInnerClass local = new LocalInnerClass();
        local.print();
    }
}

public class InnerClassExample {
    public static void main(String[] args) {
        OuterClass outer = new OuterClass();
        OuterClass.InnerClass inner = outer.new InnerClass();
        inner.display();

        OuterClass.StaticNestedClass staticNested = new OuterClass.StaticNestedClass();
        staticNested.show();

        outer.method();
    }
}
```

### 16. What is the Difference Between Shallow Copy and Deep Copy?

- **Shallow Copy**: Copies the object’s references but not the actual objects they refer to. Changes to referenced objects affect both the original and the copied object.

- **Deep Copy**: Copies the object and all objects referenced by it, creating a completely independent clone. Changes to the copied object do not affect the original.

**Code Snippet**:
```java
class Address {
    String city;

    Address(String city) {
        this.city = city;
    }
}

class Person implements Cloneable {
    String name;
    Address address;

    Person(String name, Address address) {
        this.name = name;
        this.address = address;
    }

    // Shallow copy
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    // Deep copy
    protected Person deepClone() throws CloneNotSupportedException {
        Person cloned = (Person) super.clone();
        cloned.address = new Address(this.address.city); // Deep copy of Address
        return cloned;
    }
}

public class CopyExample {
    public static void main(String[] args) {
        Address address = new Address("New York");
        Person person1 = new Person("John", address);

        try {
            Person person2 = (Person) person1.clone(); // Shallow copy
            Person person3 = person1.deepClone(); // Deep copy

            System.out.println("Person1 address: " + person1.address.city);
            System.out.println("Person2 address: " + person2.address.city); // Same as person1
            System.out.println("Person3 address: " + person3.address.city); // Different object

            person2.address.city = "Los Angeles";
            System.out.println("Person1 address after modifying person2: " + person1.address.city); // Affected
            System.out.println("Person3 address after modifying person2: " + person3.address.city); // Unaffected
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}
```

### 17. Explain the Use of `static` Keyword

The `static` keyword in Java is used to declare class-level variables and methods that belong to the class rather than to instances of the class.

 It is used for:
- **Static Variables**: Shared among all instances of the class.
- **Static Methods**: Can be called without creating an instance of the class.
- **Static Blocks**: Used for static initialization code.

**Code Snippet**:
```java
class Counter {
    static int count = 0; // Static variable

    static void increment() { // Static method
        count++;
    }

    static {
        System.out.println("Static block executed");
    }
}

public class StaticKeywordExample {
    public static void main(String[] args) {
        Counter.increment();
        System.out.println("Count: " + Counter.count); // Accessing static variable
    }
}
```

### 18. What is the Difference Between `String`, `StringBuffer`, and `StringBuilder`?

- **`String`**: Immutable sequence of characters. Any modification creates a new `String` object.

- **`StringBuffer`**: Mutable sequence of characters. It allows modification of the string without creating a new object.

- **`StringBuilder`**: Similar to `StringBuffer` but not synchronized, making it faster. It is used for single-threaded scenarios.

**Code Snippet**:
```java
public class StringBufferBuilderExample {
    public static void main(String[] args) {
        // String (Immutable)
        String str = "Hello";
        str = str.concat(" World");
        System.out.println("String: " + str);

        // StringBuffer (Mutable and synchronized)
        StringBuffer sb = new StringBuffer("Hello");
        sb.append(" World");
        System.out.println("StringBuffer: " + sb.toString());

        // StringBuilder (Mutable and not synchronized)
        StringBuilder sbuilder = new StringBuilder("Hello");
        sbuilder.append(" World");
        System.out.println("StringBuilder: " + sbuilder.toString());
    }
}
```

### 19. Explain Any Design Pattern You Are Familiar With (e.g., Singleton, Factory, Observer)

**Design Pattern**: Singleton Pattern

**Singleton Pattern** ensures that a class has only one instance and provides a global point of access to that instance. It's used when exactly one instance of a class is needed to coordinate actions across the system.

**Code Snippet**:
```java
public class Singleton {
    private static Singleton instance;

    // Private constructor prevents instantiation from other classes
    private Singleton() {}

    // Public method to provide access to the instance
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    public void showMessage() {
        System.out.println("Hello from Singleton!");
    }
}

public class SingletonDemo {
    public static void main(String[] args) {
        Singleton singleton = Singleton.getInstance();
        singleton.showMessage();
    }
}
```

### 20. How Would You Design a Parking Lot System Using OOP Concepts?

To design a parking lot system, you can use OOP concepts like classes, inheritance, and encapsulation.

**Design**:
1. **`ParkingLot`**: Manages parking spots.
2. **`ParkingSpot`**: Represents a single parking spot.
3. **`Vehicle`**: Base class for different vehicle types.
4. **`Car` and `Motorcycle`**: Inherit from `Vehicle`.

**Code Snippet**:
```java
import java.util.ArrayList;
import java.util.List;

class ParkingSpot {
    private boolean isOccupied = false;
    private Vehicle vehicle;

    public boolean isOccupied() {
        return isOccupied;
    }

    public void park(Vehicle vehicle) {
        this.vehicle = vehicle;
        isOccupied = true;
    }

    public void leave() {
        vehicle = null;
        isOccupied = false;
    }

    public Vehicle getVehicle() {
        return vehicle;
    }
}

abstract class Vehicle {
    private String licensePlate;

    public Vehicle(String licensePlate) {
        this.licensePlate = licensePlate;
    }

    public String getLicensePlate() {
        return licensePlate;
    }
}

class Car extends Vehicle {
    public Car(String licensePlate) {
        super(licensePlate);
    }
}

class Motorcycle extends Vehicle {
    public Motorcycle(String licensePlate) {
        super(licensePlate);
    }
}

class ParkingLot {
    private List<ParkingSpot> spots;

    public ParkingLot(int numberOfSpots) {
        spots = new ArrayList<>();
        for (int i = 0; i < numberOfSpots; i++) {
            spots.add(new ParkingSpot());
        }
    }

    public boolean parkVehicle(Vehicle vehicle) {
        for (ParkingSpot spot : spots) {
            if (!spot.isOccupied()) {
                spot.park(vehicle);
                return true;
            }
        }
        return false;
    }

    public void leaveParkingSpot(Vehicle vehicle) {
        for (ParkingSpot spot : spots) {
            if (spot.isOccupied() && spot.getVehicle().equals(vehicle)) {
                spot.leave();
                return;
            }
        }
    }
}

public class ParkingLotDemo {
    public static void main(String[] args) {
        ParkingLot lot = new ParkingLot(5);

        Vehicle car = new Car("123ABC");
        Vehicle motorcycle = new Motorcycle("456DEF");

        lot.parkVehicle(car);
        lot.parkVehicle(motorcycle);

        System.out.println("Car parked: " + lot.parkVehicle(car)); // Should be false, already parked

        lot.leaveParkingSpot(car);
        System.out.println("Car left: " + lot.parkVehicle(car)); // Should be true
    }
}
```

### 21. Given a Problem, How Would You Approach It Using OOP Principles?

1. **Identify the Problem**: Define the problem clearly.
2. **Define the Objects**: Identify the key objects or entities involved.
3. **Define Classes**: Create classes for each object/entity, including attributes and methods.
4. **Establish Relationships**: Determine how these classes interact with each other (e.g., inheritance, composition).
5. **Encapsulation**: Ensure that data is encapsulated within classes, exposing only necessary methods.
6. **Polymorphism**: Use polymorphism to allow different classes to be treated as instances of a common superclass.
7. **Design and Implement**: Write code based on the designed classes and relationships.

**Example Problem**: Implementing a simple library system.
**Approach**:
1. **Classes**: `Library`, `Book`, `Member`, `Loan`.
2. **Attributes**: `Library` holds `Books` and `Members`.
3. **Methods**: `Library` can lend books, register members, etc.
4. **Encapsulation**: Keep details of `Book` and `Member` private.

**Code Snippet**:
```java
import java.util.ArrayList;
import java.util.List;

class Book {
    private String title;
    private boolean isAvailable = true;

    public Book(String title) {
        this.title = title;
    }

    public String getTitle() {
        return title;
    }

    public boolean isAvailable() {
        return isAvailable;
    }

    public void setAvailable(boolean available) {
        isAvailable = available;
    }
}

class Member {
    private String name;

    public Member(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

class Library {
    private List<Book> books = new ArrayList<>();
    private List<Member> members = new ArrayList<>();

    public void addBook(Book book) {
        books.add(book);
    }

    public void addMember(Member member) {
        members.add(member);
    }

    public boolean lendBook(String title, Member member) {
        for (Book book : books) {
            if (book.getTitle().equals(title) && book.isAvailable()) {
                book.setAvailable(false);
                System.out.println("Book lent to " + member.getName());
                return true;
            }
        }
        System.out.println("Book not available");
        return false;
    }
}

public class LibraryDemo {
    public static void main(String[] args) {
        Library library = new Library();

        Book book1 = new Book("Java Programming");
        Member member1 = new Member("Alice");

        library.addBook(book1);
        library.addMember(member1);

        library.lendBook("Java Programming", member1);
    }
}
```

### 22. How Would You Implement a Shopping Cart Using OOP Concepts?

1. **Classes**: `ShoppingCart`, `Product`, `CartItem`.
2. **Attributes**: `ShoppingCart` holds `CartItems`.
3. **Methods**: Add items to the cart, remove items, calculate total price.

**Code Snippet**:
```java
import java.util.ArrayList;
import java.util.List;

class Product {
    private String name;
    private double price;

    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }
}

class CartItem {
    private Product product;
    private int quantity;

    public CartItem(Product product, int quantity) {
        this.product = product;
        this.quantity = quantity;
    }

    public double getTotalPrice() {
        return product.getPrice() * quantity;
    }

    public Product getProduct() {
        return product;
    }
}

class ShoppingCart {
    private List<CartItem> items = new ArrayList<>();

    public void addItem(Product product, int quantity) {
        items.add(new CartItem(product, quantity));
    }

    public void removeItem(Product product) {
        items.removeIf(item -> item.getProduct().equals(product));
    }

    public double getTotalAmount() {
        return items.stream().mapToDouble(CartItem::getTotalPrice).sum();
    }
}

public class ShoppingCartDemo {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();
        
        Product product1 = new Product("Laptop", 1000.00);
        Product product2 = new Product("Mouse", 25.00);

        cart.addItem(product1, 1);
        cart.addItem(product2, 2);

        System.out.println("Total Amount: " + cart.getTotalAmount());

        cart.removeItem(product2);
        System.out.println("Total Amount after removing Mouse: " + cart.getTotalAmount());
    }
}
```

### 23. Explain the Concept of Generics

**Generics** allow you to create classes, interfaces, and methods with a placeholder for types. It provides stronger type checks at compile time and eliminates the need for type casting.

**Code Snippet**:
```java
// Generic class
class Box<T> {
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
        // Using Box with Integer type
        Box<Integer> integerBox = new Box<>();
        integerBox.setValue(123);
        System.out.println("Integer value: " + integerBox.getValue());

        // Using Box with String type
        Box<String> stringBox = new Box<>();
        stringBox.setValue("Hello Generics");
        System.out.println("String value: " + stringBox.getValue());
    }
}
```

### 24. What is Type Erasure?

**Type Erasure** is a process that Java uses

 to remove generic type information during runtime. This ensures that generic code is backward compatible with older versions of Java. After compilation, the generic type information is removed, and the code operates using raw types.

**Explanation**:
- **Compile-time**: Generics provide compile-time type safety.
- **Runtime**: The generic type information is erased, and type checks are performed using the raw type.

**Code Snippet**:
```java
import java.util.ArrayList;
import java.util.List;

public class TypeErasureExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Hello");

        // Type Erasure: The list is treated as List<Object> at runtime
        for (Object item : list) {
            System.out.println(item);
        }
    }
}
```

### 25. Explain the Concept of Annotations

**Annotations** are metadata in Java that provide data about a program but are not part of the program itself. They are used to provide information to the compiler or to be used by the runtime environment. Annotations do not change the behavior of the code but can be used for various purposes such as code analysis, generation, and configuration.

**Common Annotations**:
- `@Override`: Indicates that a method is overriding a method in a superclass.
- `@Deprecated`: Marks a method or class as deprecated.
- `@SuppressWarnings`: Suppresses compiler warnings.

**Code Snippet**:
```java
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;

// Custom annotation
@Retention(RetentionPolicy.RUNTIME)
@interface MyAnnotation {
    String value();
}

class AnnotatedClass {
    @MyAnnotation("This is a custom annotation")
    public void myMethod() {
        System.out.println("Method with custom annotation");
    }
}

public class AnnotationExample {
    public static void main(String[] args) throws Exception {
        AnnotatedClass obj = new AnnotatedClass();
        obj.myMethod();
        
        // Accessing annotation at runtime
        MyAnnotation annotation = obj.getClass().getMethod("myMethod").getAnnotation(MyAnnotation.class);
        System.out.println("Annotation value: " + annotation.value());
    }
}
```

### 26. What is the Difference Between Checked and Unchecked Exceptions?

**Checked Exceptions**:
- Checked at compile time.
- Must be either caught or declared in the method using `throws`.
- Examples: `IOException`, `SQLException`.

**Unchecked Exceptions**:
- Checked at runtime.
- Do not need to be explicitly caught or declared.
- Extend `RuntimeException`.
- Examples: `NullPointerException`, `ArrayIndexOutOfBoundsException`.

**Code Snippet**:
```java
// Checked Exception Example
import java.io.File;
import java.io.FileReader;
import java.io.IOException;

public class CheckedExceptionExample {
    public static void readFile() throws IOException {
        File file = new File("nonexistentfile.txt");
        FileReader fr = new FileReader(file); // Throws IOException
        fr.close();
    }

    public static void main(String[] args) {
        try {
            readFile();
        } catch (IOException e) {
            System.out.println("Checked exception caught: " + e.getMessage());
        }
    }
}

// Unchecked Exception Example
public class UncheckedExceptionExample {
    public static void main(String[] args) {
        int[] array = new int[5];
        try {
            int value = array[10]; // Throws ArrayIndexOutOfBoundsException
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Unchecked exception caught: " + e.getMessage());
        }
    }
}
```

### 27. Explain the Use of `throws` and `try-catch` Blocks

**`throws`**:
- Used in method signatures to declare that a method can throw certain types of exceptions.
- Indicates that the method may throw an exception, and it must be handled by the calling method.

**`try-catch` Blocks**:
- Used to handle exceptions that occur during the execution of a block of code.
- The `try` block contains code that might throw an exception.
- The `catch` block handles the exception if it occurs.

**Code Snippet**:
```java
// Example using throws and try-catch
import java.io.File;
import java.io.FileReader;
import java.io.IOException;

public class ThrowsAndTryCatchExample {
    public static void readFile() throws IOException {
        File file = new File("example.txt");
        FileReader fr = new FileReader(file); // Throws IOException
        fr.close();
    }

    public static void main(String[] args) {
        try {
            readFile();
        } catch (IOException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }
}
```

### 28. What is the Difference Between `throw` and `throws` Keywords?

**`throw`**:
- Used to explicitly throw an exception from a method or block of code.
- Can be used to throw both checked and unchecked exceptions.

**`throws`**:
- Used in a method signature to declare that a method can throw certain exceptions.
- It is a way of specifying that a method might throw exceptions that need to be handled by the caller.

**Code Snippet**:
```java
// Using throw
public class ThrowExample {
    public static void validate(int age) {
        if (age < 18) {
            throw new IllegalArgumentException("Age must be at least 18"); // throw keyword
        }
    }

    public static void main(String[] args) {
        try {
            validate(16);
        } catch (IllegalArgumentException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }
}

// Using throws
public class ThrowsExample {
    public static void mayThrowException() throws IOException {
        throw new IOException("IOException occurred"); // throws keyword
    }

    public static void main(String[] args) {
        try {
            mayThrowException();
        } catch (IOException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }
}
```