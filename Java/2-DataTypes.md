# Data Types

### 1. Different Types of Data Types in Java

Java data types are classified into two main categories:

**Primitive Data Types:**
- `byte`
- `short`
- `int`
- `long`
- `float`
- `double`
- `char`
- `boolean`

**Non-Primitive Data Types (Reference Types):**
- `String`
- Arrays
- Classes and Objects
- Interfaces

### 2. Difference Between Primitive and Non-Primitive Data Types

**Primitive Data Types:**
- **Definition**: Directly hold data values.
- **Memory Allocation**: Fixed size.
- **Examples**: `int`, `char`, `boolean`.

**Non-Primitive Data Types:**
- **Definition**: Refer to objects and are used to store references to data.
- **Memory Allocation**: Variable size, depending on the object.
- **Examples**: `String`, Arrays, Custom Classes.

**Code Snippet**:
```java
public class DataTypeExample {
    public static void main(String[] args) {
        // Primitive data types
        int num = 10; // Holds an integer value directly
        String text = "Hello"; // Non-primitive data type (reference type)

        System.out.println("Primitive int: " + num);
        System.out.println("Non-primitive String: " + text);
    }
}
```

### 3. Explanation of Primitive Data Types and Their Memory Usage

**Primitive Data Types**:

- **byte**: 8-bit integer
  ```java
  byte b = 100; // Memory: 1 byte
  ```

- **short**: 16-bit integer
  ```java
  short s = 10000; // Memory: 2 bytes
  ```

- **int**: 32-bit integer
  ```java
  int i = 100000; // Memory: 4 bytes
  ```

- **long**: 64-bit integer
  ```java
  long l = 10000000000L; // Memory: 8 bytes
  ```

- **float**: Single-precision 32-bit floating point
  ```java
  float f = 10.5f; // Memory: 4 bytes
  ```

- **double**: Double-precision 64-bit floating point
  ```java
  double d = 10.5; // Memory: 8 bytes
  ```

- **char**: 16-bit Unicode character
  ```java
  char c = 'A'; // Memory: 2 bytes
  ```

- **boolean**: Represents true or false (implementation-dependent size)
  ```java
  boolean b = true; // Memory: 1 byte (typically)
  ```

### 4. When to Use `int` vs `long`

**Use `int`**:
- When the value to be stored falls within the range of -2^31 to 2^31-1 (from -2,147,483,648 to 2,147,483,647).
- More memory-efficient compared to `long`.

**Use `long`**:
- When the value exceeds the range of `int` (for values larger than 2,147,483,647).
- Useful for representing larger numbers (e.g., for timestamps, large calculations).

**Code Snippet**:
```java
public class IntVsLongExample {
    public static void main(String[] args) {
        int intValue = 2147483647; // Maximum value for int
        long longValue = 9223372036854775807L; // Maximum value for long

        System.out.println("Int value: " + intValue);
        System.out.println("Long value: " + longValue);
    }
}
```

### 5. Representation of Characters Using `char`

In Java, characters are represented using the `char` data type, which stores a single 16-bit Unicode character.

**Code Snippet**:
```java
public class CharExample {
    public static void main(String[] args) {
        char letter = 'A'; // Unicode value for 'A' is 65
        char symbol = '#'; // Unicode value for '#' is 35

        System.out.println("Character letter: " + letter);
        System.out.println("Character symbol: " + symbol);
    }
}
```

### 6. Default Value for a `boolean` Variable

The default value for a `boolean` variable is `false`.

**Code Snippet**:
```java
public class DefaultBooleanExample {
    public static void main(String[] args) {
        boolean defaultBoolean = false; // Default value for boolean

        System.out.println("Default boolean value: " + defaultBoolean);
    }
}
```

### 7. Non-Primitive Data Types

**Non-Primitive Data Types** (Reference Types) include:

- **String**: Represents a sequence of characters.
- **Arrays**: Containers for holding multiple values of the same type.
- **Classes**: User-defined blueprints for objects.
- **Interfaces**: Abstract types used to specify a set of methods that a class must implement.

**Code Snippet**:
```java
public class NonPrimitiveExample {
    public static void main(String[] args) {
        // String example
        String str = "Hello, World!";

        // Array example
        int[] numbers = {1, 2, 3, 4, 5};

        // Displaying String and Array
        System.out.println("String: " + str);
        System.out.print("Array elements: ");
        for (int number : numbers) {
            System.out.print(number + " ");
        }
    }
}
```

### 8. Examples of Non-Primitive Data Types

**Examples**:
- `String`
- Arrays (e.g., `int[]`, `String[]`)
- User-defined classes (e.g., `Person`, `Car`)

**Code Snippet**:
```java
public class NonPrimitiveExamples {
    public static void main(String[] args) {
        // String example
        String greeting = "Welcome to Java!";

        // Array example
        String[] names = {"Alice", "Bob", "Charlie"};

        // User-defined class example
        Person person = new Person("John", 30);

        System.out.println("Greeting: " + greeting);
        System.out.println("Names: ");
        for (String name : names) {
            System.out.println(name);
        }
        System.out.println("Person: " + person.getName() + ", Age: " + person.getAge());
    }
}

// User-defined class
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
```

### 9. Concept of Wrapper Classes in Java

Wrapper classes are used to convert primitive data types into objects. Each primitive type has a corresponding wrapper class in the `java.lang` package.

**Wrapper Classes**:
- `Byte` for `byte`
- `Short` for `short`
- `Integer` for `int`
- `Long` for `long`
- `Float` for `float`
- `Double` for `double`
- `Character` for `char`
- `Boolean` for `boolean`

**Code Snippet**:
```java
public class WrapperClassExample {
    public static void main(String[] args) {
        // Creating wrapper objects
        Integer intObj = 100; // Auto-boxing
        Double doubleObj = 99.99;
        Character charObj = 'A';

        // Using wrapper class methods
        System.out.println("Integer object: " + intObj);
        System.out.println("Double object: " + doubleObj);
        System.out.println("Character object: " + charObj);

        // Converting wrapper to primitive type
        int intValue = intObj.intValue();
        double doubleValue = doubleObj.doubleValue();
        char charValue = charObj.charValue();

        System.out.println("Primitive int: " + intValue);
        System.out.println("Primitive double: " + doubleValue);
        System.out.println("Primitive char: " + charValue);
    }
}
```

### 10. Converting a String to a Primitive Data Type

You can convert a `String` to a primitive data type using the wrapper class methods. For example:

- **Convert `String` to `int`**:
  ```java
  public class StringToPrimitive {
      public static void main(String[] args) {
          String str = "123";
          int number = Integer.parseInt(str); // Convert String to int
          System.out.println("Converted int: " + number);
      }
  }
  ```

- **Convert `String` to `double`**:
  ```java
  public class StringToDouble {
      public static void main(String[] args) {
          String str = "123.45";
          double number = Double.parseDouble(str); // Convert String to double
          System.out.println("Converted double: " + number);
      }
  }
  ```

### 11. Autoboxing and Unboxing in Java

**Autoboxing** is the automatic conversion of primitive types to their corresponding wrapper classes (e.g., `int` to `Integer`). **Unboxing** is the reverse process: converting a wrapper class to its corresponding primitive type.

**Autoboxing Example**:
```java
public class AutoboxingExample {
    public static void main(String[] args) {
        int primitiveInt = 10;
        Integer wrapperInt = primitiveInt; // Autoboxing
        System.out.println("Wrapper Integer: " + wrapperInt);
    }
}
```

**Unboxing Example**:
```java
public class UnboxingExample {
    public static void main(String[] args) {
        Integer wrapperInt = 10;
        int primitiveInt = wrapperInt; // Unboxing
        System.out.println("Primitive int: " + primitiveInt);
    }
}
```

### 12. Primitive Data Type Casting

**Casting** is used to convert one primitive data type to another. This can be either **implicit** (automatic) or **explicit** (manual).

**Implicit Casting** (Widening Conversion):
- Converting a smaller type to a larger type (e.g., `int` to `double`).
  ```java
  public class WideningCasting {
      public static void main(String[] args) {
          int intVal = 100;
          double doubleVal = intVal; // Implicit casting
          System.out.println("Double value: " + doubleVal);
      }
  }
  ```

**Explicit Casting** (Narrowing Conversion):
- Converting a larger type to a smaller type (e.g., `double` to `int`).
  ```java
  public class NarrowingCasting {
      public static void main(String[] args) {
          double doubleVal = 100.99;
          int intVal = (int) doubleVal; // Explicit casting
          System.out.println("Int value: " + intVal);
      }
  }
  ```

### 13. String Class and Its Immutability

The `String` class in Java represents a sequence of characters. Strings are immutable, meaning once a `String` object is created, it cannot be modified. Any operation that seems to modify a string actually creates a new `String` object.

**Code Snippet**:
```java
public class StringImmutability {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = str1.concat(" World"); // Creates a new String object

        System.out.println("Original String: " + str1); // Output: Hello
        System.out.println("Modified String: " + str2); // Output: Hello World
    }
}
```

### 14. Handling Floating-Point Numbers

Java handles floating-point numbers using the `float` and `double` types. These types may introduce precision errors due to their approximate nature (IEEE 754 standard).

**Code Snippet**:
```java
public class FloatingPointExample {
    public static void main(String[] args) {
        float floatVal = 0.1f;
        double doubleVal = 0.1;

        System.out.println("Float value: " + floatVal);
        System.out.println("Double value: " + doubleVal);

        // Precision issue example
        System.out.println("0.1f + 0.2f: " + (floatVal + 0.2f));
        System.out.println("0.1 + 0.2: " + (doubleVal + 0.2));
    }
}
```

### 15. Significance of `null` Value in Java

The `null` value represents the absence of a value or object. It can be assigned to any reference type but not to primitive data types. It is used to indicate that a reference variable is not currently pointing to any object.

**Code Snippet**:
```java
public class NullValueExample {
    public static void main(String[] args) {
        String str = null; // str does not point to any object
        int[] array = null; // array does not point to any object

        System.out.println("String value: " + str); // Output: null
        System.out.println("Array length: " + (array != null ? array.length : "Not initialized"));
    }
}
```

### 16. Scenario-Based Questions

**17. Data Type for Storing Dimensions**

For storing dimensions like width and height, use `double` if precision is important (e.g., measurements in meters). Use `int` if the dimensions are whole numbers and precision is less critical.

**Code Snippet**:
```java
public class AreaCalculation {
    public static void main(String[] args) {
        double width = 10.5; // Dimensions with decimal values
        double height = 20.3;
        double area = width * height;

        System.out.println("Area: " + area);
    }
}
```

**18. Ensuring Valid Integer Input**

To ensure that user input for age is a valid integer, use `try-catch` to handle `NumberFormatException` and validate the input.

**Code Snippet**:
```java
import java.util.Scanner;

public class AgeValidation {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int age = 0;
        boolean valid = false;

        while (!valid) {
            System.out.print("Enter your age: ");
            String input = scanner.nextLine();

            try {
                age = Integer.parseInt(input);
                if (age >= 0) {
                    valid = true; // Valid input
                } else {
                    System.out.println("Age cannot be negative. Please try again.");
                }
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a valid integer.");
            }
        }

        System.out.println("Your age is: " + age);
        scanner.close();
    }
}
```