# Streams

### 1. What is a Stream in Java? Explain its characteristics.

**Answer:**
A Stream in Java is a sequence of elements that supports various methods for processing collections of objects. Streams are part of the Java 8 `java.util.stream` package and allow functional-style operations on sequences of elements, such as map-reduce transformations. 

**Characteristics:**
- **Non-storage**: Streams do not store data. They are simply views of data and can be considered as a pipeline of operations.
- **Functional Programming**: Streams support functional programming features like lambda expressions.
- **Lazy Evaluation**: Operations on streams are performed lazily, meaning they are not executed until a terminal operation is invoked.
- **Immutable**: Streams do not modify the underlying data structure; they produce new streams.

**Code Snippet:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");

        // Creating a stream from a list
        names.stream()
             .filter(name -> name.startsWith("A"))
             .forEach(System.out::println); // Outputs: Alice
    }
}
```

### 2. Differentiate between a Stream and a Collection.

**Answer:**
- **Collection**:
  - **Purpose**: Holds data in memory.
  - **Mutable**: Collections can be modified (add/remove elements).
  - **Traversal**: You can iterate over elements, but cannot perform operations like filtering or mapping directly.

- **Stream**:
  - **Purpose**: Provides a pipeline for processing data.
  - **Immutable**: Streams do not alter the source collection but produce new streams.
  - **Operations**: Allows functional-style operations like filtering, mapping, and reducing.

**Code Snippet:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamVsCollection {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Collection operation: Iterating
        for (String name : names) {
            System.out.println(name);
        }

        // Stream operation: Filtering and mapping
        names.stream()
             .filter(name -> name.length() > 3)
             .map(String::toUpperCase)
             .forEach(System.out::println); // Outputs: ALICE, CHARLIE
    }
}
```

### 3. Explain the Difference Between Intermediate and Terminal Operations.

**Answer:**
- **Intermediate Operations**: These operations transform a stream into another stream and are lazy, meaning they are not executed until a terminal operation is invoked. Examples include `filter()`, `map()`, and `sorted()`.

- **Terminal Operations**: These operations produce a result or a side-effect and terminate the stream pipeline. They force the processing of the stream. Examples include `collect()`, `forEach()`, and `reduce()`.

**Code Snippet:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamOperations {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Intermediate operations
        numbers.stream()
               .filter(n -> n % 2 == 0) // filter
               .map(n -> n * n) // map
               .sorted(); // sorted

        // Terminal operation
        long count = numbers.stream()
                            .filter(n -> n % 2 == 0)
                            .count(); // count
        System.out.println("Count of even numbers: " + count); // Outputs: 2
    }
}
```

### 4. What Is the Difference Between `map` and `flatMap`?

**Answer:**
- **`map`**: Transforms each element of the stream into another element. It applies a function to each element and returns a stream of the transformed elements.

- **`flatMap`**: Transforms each element into a stream of objects and then flattens the resulting streams into a single stream. It's useful for dealing with nested structures or multiple elements.

**Code Snippet:**

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class MapVsFlatMap {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob");

        // Using map
        List<Integer> nameLengths = names.stream()
                                         .map(String::length)
                                         .collect(Collectors.toList());
        System.out.println(nameLengths); // Outputs: [5, 3]

        // Using flatMap
        List<String> letters = names.stream()
                                    .flatMap(name -> Arrays.stream(name.split("")))
                                    .collect(Collectors.toList());
        System.out.println(letters); // Outputs: [A, l, i, c, e, B, o, b]
    }
}
```

### 5. How Do You Create a Stream from a List, Array, or Other Data Structures?

**Answer:**
- **From a List**: Use the `stream()` method.
- **From an Array**: Use `Arrays.stream(array)`.
- **From Other Data Structures**: Use appropriate methods or convert to a list first.

**Code Snippet:**

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Stream;

public class CreateStream {
    public static void main(String[] args) {
        // From a List
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
        Stream<String> nameStream = names.stream();

        // From an Array
        String[] namesArray = {"Alice", "Bob", "Charlie"};
        Stream<String> arrayStream = Arrays.stream(namesArray);

        // From other data structures (e.g., Set)
        Set<String> nameSet = new HashSet<>(names);
        Stream<String> setStream = nameSet.stream();
    }
}
```

### 6. Explain the Use of `filter`, `map`, `flatMap`, `distinct`, `sorted`, and `limit` Operations.

**Answer:**

- **`filter`**: Filters elements based on a predicate. It retains elements that satisfy the condition.

  ```java
  List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
  numbers.stream()
         .filter(n -> n % 2 == 0)
         .forEach(System.out::println); // Outputs: 2, 4
  ```

- **`map`**: Applies a function to each element and returns a stream of the results.

  ```java
  List<String> names = Arrays.asList("Alice", "Bob");
  names.stream()
       .map(String::toUpperCase)
       .forEach(System.out::println); // Outputs: ALICE, BOB
  ```

- **`flatMap`**: Maps each element to a stream and flattens the result.

  ```java
  List<String> sentences = Arrays.asList("Hello World", "Java Streams");
  sentences.stream()
           .flatMap(sentence -> Arrays.stream(sentence.split(" ")))
           .forEach(System.out::println); // Outputs: Hello, World, Java, Streams
  ```

- **`distinct`**: Removes duplicate elements from the stream.

  ```java
  List<Integer> numbers = Arrays.asList(1, 2, 2, 3, 4, 4, 5);
  numbers.stream()
         .distinct()
         .forEach(System.out::println); // Outputs: 1, 2, 3, 4, 5
  ```

- **`sorted`**: Sorts the elements of the stream. It can take a comparator for custom sorting.

  ```java
  List<String> names = Arrays.asList("Charlie", "Alice", "Bob");
  names.stream()
       .sorted()
       .forEach(System.out::println); // Outputs: Alice, Bob, Charlie
  ```

- **`limit`**: Limits the number of elements in the stream.

  ```java
  List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
  numbers.stream()
         .limit(3)
         .forEach(System.out::println); // Outputs: 1, 2, 3
  ```

### 7. How do you perform custom sorting on a Stream?

**Answer:**
To perform custom sorting on a Stream, you can use the `sorted` method with a `Comparator`. The `Comparator` allows you to define custom sorting logic.

**Code Snippet:**

```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

public class CustomSorting {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Charlie", "Alice", "Bob");

        // Custom sorting: sort by length of strings, then alphabetically
        names.stream()
             .sorted(Comparator.comparing(String::length).thenComparing(String::compareTo))
             .forEach(System.out::println); // Outputs: Bob, Alice, Charlie
    }
}
```

### 8. What is lazy evaluation in Streams? Explain its benefits.

**Answer:**
Lazy evaluation in Streams means that intermediate operations (e.g., `filter`, `map`) are not executed until a terminal operation (e.g., `collect`, `forEach`) is invoked. This allows the Stream API to optimize processing and avoid unnecessary computations.

**Benefits:**
- **Efficiency**: Only the necessary elements are processed. Intermediate operations are combined and optimized.
- **Performance**: Reduces overhead by processing elements in a single pass when possible.
- **Flexibility**: Allows the Stream to be constructed incrementally and processed on demand.

**Code Snippet:**

```java
import java.util.Arrays;
import java.util.List;

public class LazyEvaluation {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Lazy evaluation: filter and map are not executed until terminal operation
        numbers.stream()
               .filter(n -> {
                   System.out.println("Filtering: " + n);
                   return n % 2 == 0;
               })
               .map(n -> {
                   System.out.println("Mapping: " + n);
                   return n * n;
               })
               .forEach(System.out::println); // Outputs: Filtering, Mapping, and result
    }
}
```

### 9. Describe the purpose of `collect`, `reduce`, `forEach`, `findAny`, `findFirst`, and `allMatch` operations.

**Answer:**

- **`collect`**: Transforms the elements of a Stream into a collection or other result. It's a terminal operation.

  ```java
  import java.util.Arrays;
  import java.util.List;
  import java.util.stream.Collectors;

  public class CollectExample {
      public static void main(String[] args) {
          List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
          List<String> upperNames = names.stream()
                                         .map(String::toUpperCase)
                                         .collect(Collectors.toList());
          System.out.println(upperNames); // Outputs: [ALICE, BOB, CHARLIE]
      }
  }
  ```

- **`reduce`**: Performs a reduction on the elements of the Stream using an associative accumulation function and returns an `Optional`.

  ```java
  import java.util.Arrays;
  import java.util.List;
  import java.util.Optional;

  public class ReduceExample {
      public static void main(String[] args) {
          List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
          Optional<Integer> sum = numbers.stream()
                                          .reduce((a, b) -> a + b);
          System.out.println(sum.orElse(0)); // Outputs: 15
      }
  }
  ```

- **`forEach`**: Performs an action for each element of the Stream. It is a terminal operation.

  ```java
  import java.util.Arrays;
  import java.util.List;

  public class ForEachExample {
      public static void main(String[] args) {
          List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
          names.stream()
               .forEach(System.out::println); // Outputs: Alice, Bob, Charlie
      }
  }
  ```

- **`findAny`**: Returns an `Optional` describing any element of the Stream. It may return different results if the Stream is unordered.

  ```java
  import java.util.Arrays;
  import java.util.List;
  import java.util.Optional;

  public class FindAnyExample {
      public static void main(String[] args) {
          List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
          Optional<String> anyName = names.stream()
                                          .findAny();
          System.out.println(anyName.orElse("No name found")); // Outputs: Any name from the list
      }
  }
  ```

- **`findFirst`**: Returns an `Optional` describing the first element of the Stream.

  ```java
  import java.util.Arrays;
  import java.util.List;
  import java.util.Optional;

  public class FindFirstExample {
      public static void main(String[] args) {
          List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
          Optional<String> firstName = names.stream()
                                            .findFirst();
          System.out.println(firstName.orElse("No name found")); // Outputs: Alice
      }
  }
  ```

- **`allMatch`**: Checks if all elements of the Stream match the given predicate. Returns a boolean.

  ```java
  import java.util.Arrays;
  import java.util.List;

  public class AllMatchExample {
      public static void main(String[] args) {
          List<Integer> numbers = Arrays.asList(2, 4, 6, 8);
          boolean allEven = numbers.stream()
                                   .allMatch(n -> n % 2 == 0);
          System.out.println(allEven); // Outputs: true
      }
  }
  ```

### 10. How Do You Use Collectors to Process Stream Elements?

**Answer:**
`Collectors` is a utility class in `java.util.stream` that provides various implementations to collect the elements of a Stream into collections, aggregations, or other results.

**Code Snippet:**

```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class CollectorsExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie");

        // Collecting into a List
        List<String> nameList = names.stream()
                                     .collect(Collectors.toList());
        System.out.println(nameList); // Outputs: [Alice, Bob, Charlie]

        // Collecting into a Set
        Set<String> nameSet = names.stream()
                                   .collect(Collectors.toSet());
        System.out.println(nameSet); // Outputs: [Alice, Bob, Charlie]

        // Collecting into a Map
        Map<Integer, String> nameMap = names.stream()
                                            .collect(Collectors.toMap(String::length, name -> name));
        System.out.println(nameMap); // Outputs: {3=Bob, 5=Alice, 7=Charlie}
    }
}
```

### 11. Explain the Difference Between `reduce` and `collect`.

**Answer:**
- **`reduce`**: 
  - Performs a reduction on the elements of the Stream using an associative accumulation function. It reduces the elements to a single result.
  - Example: Calculating the sum of a list of numbers.
  - Returns: An `Optional` containing the reduced value, or an empty `Optional` if the Stream is empty.

- **`collect`**: 
  - Converts the elements of the Stream into a different form such as a collection (e.g., `List`, `Set`, `Map`).
  - Example: Collecting elements into a `List` or `Set`.
  - Returns: The result of the collection operation, which is a concrete collection or other result type.

**Code Snippet:**

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class ReduceVsCollect {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Using reduce
        int sum = numbers.stream()
                         .reduce(0, Integer::sum);
        System.out.println("Sum: " + sum); // Outputs: 15

        // Using collect
        List<Integer> numberList = numbers.stream()
                                          .collect(Collectors.toList());
        System.out.println("List: " + numberList); // Outputs: [1, 2, 3, 4, 5]
    }
}
```