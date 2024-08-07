# Collection Framework

### 1. What is the Java Collections Framework?

**The Java Collections Framework** is a unified architecture for representing and manipulating collections of objects. It provides a set of interfaces and classes that implement common data structures and algorithms to manage groups of objects, such as lists, sets, and maps.

**Key Components**:
- **Interfaces**: Define the core data structures.
- **Implementations**: Concrete classes that provide data structure implementations.
- **Algorithms**: Static methods to perform operations like sorting and searching.

**Code Snippet** (Basic usage of the Collections Framework):
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.Map;
import java.util.Set;
import java.util.List;

public class CollectionsDemo {
    public static void main(String[] args) {
        // List example
        List<String> arrayList = new ArrayList<>();
        arrayList.add("Apple");
        arrayList.add("Banana");

        // Set example
        Set<String> hashSet = new HashSet<>();
        hashSet.add("Cat");
        hashSet.add("Dog");

        // Map example
        Map<String, Integer> hashMap = new HashMap<>();
        hashMap.put("One", 1);
        hashMap.put("Two", 2);

        // Print results
        System.out.println("List: " + arrayList);
        System.out.println("Set: " + hashSet);
        System.out.println("Map: " + hashMap);
    }
}
```

### 2. What Are the Core Interfaces in the Collections Framework?

**Core Interfaces**:
- **List**: An ordered collection that allows duplicate elements. Example implementations: `ArrayList`, `LinkedList`.
- **Set**: A collection that does not allow duplicate elements. Example implementations: `HashSet`, `TreeSet`.
- **Map**: A collection that maps keys to values, with each key associated with a single value. Example implementations: `HashMap`, `TreeMap`.
- **Queue**: A collection designed for holding elements prior to processing. Example implementations: `LinkedList`, `PriorityQueue`.

**Code Snippet** (Using core interfaces):
```java
import java.util.*;

public class CoreInterfacesDemo {
    public static void main(String[] args) {
        // List
        List<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        
        // Set
        Set<String> set = new HashSet<>();
        set.add("X");
        set.add("Y");

        // Map
        Map<String, Integer> map = new HashMap<>();
        map.put("Key1", 100);
        map.put("Key2", 200);

        // Queue
        Queue<String> queue = new LinkedList<>();
        queue.add("First");
        queue.add("Second");

        System.out.println("List: " + list);
        System.out.println("Set: " + set);
        System.out.println("Map: " + map);
        System.out.println("Queue: " + queue);
    }
}
```

### 3. Explain the Difference Between List, Set, and Map Interfaces.

- **List**: Maintains order and allows duplicates. Provides indexed access.
  - **Example**: `ArrayList`, `LinkedList`.
  - **Use Case**: When you need to store elements in a specific order and allow duplicates.

- **Set**: Does not allow duplicates and does not maintain order (except `LinkedHashSet` which maintains insertion order and `TreeSet` which sorts elements).
  - **Example**: `HashSet`, `TreeSet`.
  - **Use Case**: When you need to ensure that no duplicates are stored.

- **Map**: Stores key-value pairs with unique keys. Each key maps to exactly one value.
  - **Example**: `HashMap`, `TreeMap`.
  - **Use Case**: When you need to associate keys with values and quickly retrieve values based on keys.

**Code Snippet**:
```java
import java.util.*;

public class DifferenceDemo {
    public static void main(String[] args) {
        // List
        List<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        list.add("A");
        System.out.println("List: " + list);

        // Set
        Set<String> set = new HashSet<>();
        set.add("A");
        set.add("B");
        set.add("A");
        System.out.println("Set: " + set);

        // Map
        Map<String, String> map = new HashMap<>();
        map.put("1", "A");
        map.put("2", "B");
        map.put("1", "C"); // Overwrites value for key "1"
        System.out.println("Map: " + map);
    }
}
```

### 4. What Is the Difference Between an Array and a Collection?

- **Array**:
  - Fixed size.
  - Can hold primitive types or objects.
  - Requires manual resizing if more elements are needed.

- **Collection**:
  - Dynamic size.
  - Provides powerful methods for manipulating data (add, remove, sort, etc.).
  - Implemented as `List`, `Set`, `Map`, etc.

**Code Snippet**:
```java
import java.util.*;

public class ArrayVsCollection {
    public static void main(String[] args) {
        // Array
        int[] array = new int[3];
        array[0] = 1;
        array[1] = 2;
        array[2] = 3;
        System.out.println("Array: " + Arrays.toString(array));

        // Collection
        List<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        System.out.println("List: " + list);
    }
}
```

### 5. What Are the Advantages of Using Collections Over Arrays?

- **Dynamic Sizing**: Collections can grow and shrink dynamically.
- **Enhanced Functionality**: Collections provide methods to manipulate data (e.g., sorting, filtering).
- **Ease of Use**: Collections APIs simplify many operations, such as searching and iterating.
- **Flexibility**: Different types of collections (e.g., `List`, `Set`, `Map`) provide flexibility for various data manipulation needs.

### 6. Explain the Difference Between `ArrayList` and `LinkedList`. When Would You Use One Over the Other?

- **ArrayList**:
  - Backed by a dynamically resizable array.
  - Provides fast random access (`O(1)` time complexity for `get()`).
  - Slower insertions and deletions in the middle (`O(n)` time complexity).

- **LinkedList**:
  - Backed by a doubly-linked list.
  - Provides faster insertions and deletions in the middle (`O(1)` time complexity if the node is known).
  - Slower random access (`O(n)` time complexity for `get()`).

**Code Snippet**:
```java
import java.util.*;

public class ArrayListVsLinkedList {
    public static void main(String[] args) {
        // ArrayList
        List<String> arrayList = new ArrayList<>();
        arrayList.add("A");
        arrayList.add("B");
        arrayList.add("C");
        System.out.println("ArrayList: " + arrayList);

        // LinkedList
        List<String> linkedList = new LinkedList<>();
        linkedList.add("A");
        linkedList.add("B");
        linkedList.add("C");
        System.out.println("LinkedList: " + linkedList);
    }
}
```

### 7. What Is the Difference Between `HashSet` and `TreeSet`? When Would You Use One Over the Other?

- **HashSet**:
  - Backed by a hash table.
  - Provides constant time complexity (`O(1)`) for basic operations (`add`, `remove`, `contains`).
  - Does not maintain order.

- **TreeSet**:
  - Backed by a red-black tree.
  - Provides `O(log n)` time complexity for basic operations.
  - Maintains elements in a sorted order.

**Code Snippet**:
```java
import java.util.*;

public class HashSetVsTreeSet {
    public static void main(String[] args) {
        // HashSet
        Set<String> hashSet = new HashSet<>();
        hashSet.add("B");
        hashSet.add("A");
        hashSet.add("C");
        System.out.println("HashSet: " + hashSet);

        // TreeSet
        Set<String> treeSet = new TreeSet<>();
        treeSet.add("B");
        treeSet.add("A");
        treeSet.add("C");
        System.out.println("TreeSet: " + treeSet);
    }
}
```

### 8. Explain the Difference Between `HashMap` and `TreeMap`. When Would You Use One Over the Other?

**`HashMap`**:
- **Implementation**: Backed by a hash table.
- **Ordering**: Does not maintain any order of keys.
- **Performance**: Provides constant-time complexity (`O(1)`) for basic operations like `put` and `get`.
- **Use Case**: When you need fast retrieval and insertion without caring about the order of keys.

**`TreeMap`**:
- **Implementation**: Backed by a Red-Black tree.
- **Ordering**: Maintains keys in a sorted order according to their natural ordering or a provided comparator.
- **Performance**: Provides `O(log n)` time complexity for basic operations due to the tree structure.
- **Use Case**: When you need a map with sorted keys.

**Code Snippet**:
```java
import java.util.*;

public class MapComparison {
    public static void main(String[] args) {
        // HashMap
        Map<String, Integer> hashMap = new HashMap<>();
        hashMap.put("Banana", 2);
        hashMap.put("Apple", 1);
        hashMap.put("Orange", 3);
        System.out.println("HashMap: " + hashMap);

        // TreeMap
        Map<String, Integer> treeMap = new TreeMap<>();
        treeMap.put("Banana", 2);
        treeMap.put("Apple", 1);
        treeMap.put("Orange", 3);
        System.out.println("TreeMap: " + treeMap);
    }
}
```

### 9. What is a `LinkedHashMap`? When Would You Use It?

**`LinkedHashMap`**:
- **Implementation**: Extends `HashMap` and maintains a doubly-linked list of entries, which preserves the insertion order of keys.
- **Ordering**: Maintains the order in which keys were inserted (or access order if specified).
- **Performance**: Provides `O(1)` time complexity for `get` and `put` operations, with the added overhead of maintaining the linked list.

**Use Case**: Use `LinkedHashMap` when you need a map that preserves the insertion order or access order of entries.

**Code Snippet**:
```java
import java.util.*;

public class LinkedHashMapDemo {
    public static void main(String[] args) {
        // LinkedHashMap
        Map<String, Integer> linkedHashMap = new LinkedHashMap<>();
        linkedHashMap.put("Banana", 2);
        linkedHashMap.put("Apple", 1);
        linkedHashMap.put("Orange", 3);
        System.out.println("LinkedHashMap: " + linkedHashMap);
    }
}
```

### 10. What is a `PriorityQueue`? Explain Its Working.

**`PriorityQueue`**:
- **Implementation**: Implements a priority heap-based queue.
- **Ordering**: Elements are ordered according to their natural ordering or by a provided comparator.
- **Functionality**: Does not permit `null` elements and offers operations like `peek`, `poll`, and `add` to access or remove the highest priority element.

**Use Case**: Use `PriorityQueue` when you need a queue with elements ordered by priority.

**Code Snippet**:
```java
import java.util.*;

public class PriorityQueueDemo {
    public static void main(String[] args) {
        // PriorityQueue
        PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();
        priorityQueue.add(5);
        priorityQueue.add(1);
        priorityQueue.add(3);

        System.out.println("PriorityQueue: " + priorityQueue);
        System.out.println("Polling elements:");
        while (!priorityQueue.isEmpty()) {
            System.out.println(priorityQueue.poll());
        }
    }
}
```

### 11. Explain the Concept of Iterator and `ListIterator`.

**Iterator**:
- **Purpose**: Provides a way to traverse a collection (e.g., `List`, `Set`) without exposing the underlying structure.
- **Methods**: `hasNext()`, `next()`, `remove()`.

**ListIterator**:
- **Purpose**: Extends `Iterator` and provides additional functionality to traverse a list in both directions (forward and backward).
- **Methods**: `hasNext()`, `next()`, `hasPrevious()`, `previous()`, `add()`, `set()`.

**Code Snippet**:
```java
import java.util.*;

public class IteratorDemo {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>(Arrays.asList("A", "B", "C"));

        // Using Iterator
        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }

        // Using ListIterator
        ListIterator<String> listIterator = list.listIterator();
        System.out.println("Forward iteration:");
        while (listIterator.hasNext()) {
            System.out.println(listIterator.next());
        }

        System.out.println("Backward iteration:");
        while (listIterator.hasPrevious()) {
            System.out.println(listIterator.previous());
        }
    }
}
```

### 12. What is Fail-Fast and Fail-Safe Iterators?

**Fail-Fast Iterators**:
- **Definition**: Fail-fast iterators immediately throw a `ConcurrentModificationException` if the collection is modified while iterating.
- **Example**: `ArrayList`, `HashSet`.

**Fail-Safe Iterators**:
- **Definition**: Fail-safe iterators work on a clone of the collection, allowing modifications without throwing an exception.
- **Example**: `ConcurrentHashMap`, `CopyOnWriteArrayList`.

**Code Snippet** (Fail-Fast Example):
```java
import java.util.*;

public class FailFastExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>(Arrays.asList("A", "B", "C"));
        Iterator<String> iterator = list.iterator();

        // Modifying collection while iterating (will throw ConcurrentModificationException)
        try {
            while (iterator.hasNext()) {
                System.out.println(iterator.next());
                list.add("D"); // This will cause ConcurrentModificationException
            }
        } catch (ConcurrentModificationException e) {
            System.out.println("Exception: " + e);
        }
    }
}
```

### 13. Explain the Concept of Generics in Collections.

**Generics**:
- **Purpose**: Provide type safety by allowing classes and methods to operate on specified types while providing compile-time type checking.
- **Usage**: Specify type parameters when declaring collections to avoid runtime `ClassCastException`.

**Code Snippet**:
```java
import java.util.*;

public class GenericsDemo {
    public static void main(String[] args) {
        // Using Generics
        List<String> stringList = new ArrayList<>();
        stringList.add("A");
        stringList.add("B");

        // Compile-time type safety
        for (String s : stringList) {
            System.out.println(s);
        }

        // Uncommenting the following line would cause a compile-time error
        // stringList.add(1); // Compile-time error: incompatible types
    }
}
```

### 14. How Does `HashMap` Work Internally? Explain Hashing and Collision Handling.

**HashMap Internals**:
- **Hashing**: Uses a hash function to compute the index in an array where the entry (key-value pair) is stored.
- **Collision Handling**: Handles collisions using linked lists or trees (when bucket size exceeds a threshold) within each index of the hash table.

**Code Snippet** (Illustration of HashMap):
```java
import java.util.*;

public class HashMapInternalDemo {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("One", 1);
        map.put("Two", 2);
        map.put("Three", 3);

        // Print HashMap
        System.out.println("HashMap: " + map);
    }
}
```

**Explanation**:
- **Hash Function**: Converts the key into an integer hash code, which determines the index in the internal array.
- **Buckets**: Collisions are resolved by linking entries in the same bucket (list or tree).

### 15. How Does `HashSet` Ensure Uniqueness?

**`HashSet`** ensures uniqueness by using a `HashMap` internally. When you add an element, it calculates the hash code of the element and uses it to determine the bucket where the element should be placed. If the element already exists in the bucket (determined by the `equals` method), it is not added again.

**Code Snippet**:
```java
import java.util.HashSet;

public class HashSetDemo {
    public static void main(String[] args) {
        HashSet<String> set = new HashSet<>();
        set.add("Apple");
        set.add("Banana");
        set.add("Apple"); // Duplicate, will not be added

        System.out.println("HashSet: " + set); // Output: [Apple, Banana]
    }
}
```

### 16. Explain the Concept of Concurrency in Collections. What Are `ConcurrentHashMap` and `CopyOnWriteArrayList`?

**Concurrency** in collections refers to the ability to handle multiple threads accessing or modifying the collection simultaneously.

- **`ConcurrentHashMap`**:
  - **Purpose**: A thread-safe variant of `HashMap` designed for high concurrency.
  - **Implementation**: Divides the map into segments or buckets that can be locked independently, allowing concurrent access to different segments.
  - **Usage**: Useful when multiple threads need to read and write to the map frequently.

- **`CopyOnWriteArrayList`**:
  - **Purpose**: A thread-safe variant of `ArrayList` where modifications (e.g., add/remove) create a new copy of the underlying array.
  - **Implementation**: The list is copied on each write operation, which makes read operations fast and thread-safe.
  - **Usage**: Suitable when there are more reads than writes.

**Code Snippet**:
```java
import java.util.concurrent.*;

public class ConcurrencyDemo {
    public static void main(String[] args) {
        // ConcurrentHashMap
        ConcurrentHashMap<String, Integer> concurrentMap = new ConcurrentHashMap<>();
        concurrentMap.put("Key1", 1);
        concurrentMap.put("Key2", 2);
        System.out.println("ConcurrentHashMap: " + concurrentMap);

        // CopyOnWriteArrayList
        CopyOnWriteArrayList<String> copyOnWriteList = new CopyOnWriteArrayList<>();
        copyOnWriteList.add("Element1");
        copyOnWriteList.add("Element2");
        System.out.println("CopyOnWriteArrayList: " + copyOnWriteList);
    }
}
```

### 17. How Do You Sort a List of Custom Objects?

To sort a `List` of custom objects, you need to implement the `Comparable` interface in your custom class or use a `Comparator`.

**Using `Comparable`**:
- Implement the `Comparable` interface in the custom class and override the `compareTo` method.

**Using `Comparator`**:
- Define a `Comparator` and pass it to the `Collections.sort` method.

**Code Snippet**:
```java
import java.util.*;

class Person implements Comparable<Person> {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Person other) {
        return Integer.compare(this.age, other.age); // Sorting by age
    }

    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}

public class SortingDemo {
    public static void main(String[] args) {
        List<Person> people = new ArrayList<>();
        people.add(new Person("Alice", 30));
        people.add(new Person("Bob", 25));
        people.add(new Person("Charlie", 35));

        // Sorting using Comparable
        Collections.sort(people);
        System.out.println("Sorted by age (Comparable): " + people);

        // Sorting using Comparator
        Comparator<Person> nameComparator = Comparator.comparing(p -> p.name);
        Collections.sort(people, nameComparator);
        System.out.println("Sorted by name (Comparator): " + people);
    }
}
```

### 18. What Is the Difference Between `Comparable` and `Comparator`?

- **`Comparable`**:
  - **Purpose**: Defines the natural ordering of objects in a class.
  - **Implementation**: Implement the `Comparable` interface and override the `compareTo` method.
  - **Usage**: Used when you want to define a default sorting order for your objects.

- **`Comparator`**:
  - **Purpose**: Defines multiple sorting orders outside of the class.
  - **Implementation**: Implement the `Comparator` interface and override the `compare` method.
  - **Usage**: Used for sorting objects in different ways or when the class doesn’t implement `Comparable`.

**Code Snippet**:
```java
import java.util.*;

class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}

public class ComparatorDemo {
    public static void main(String[] args) {
        List<Person> people = new ArrayList<>();
        people.add(new Person("Alice", 30));
        people.add(new Person("Bob", 25));
        people.add(new Person("Charlie", 35));

        // Comparator for sorting by name
        Comparator<Person> nameComparator = Comparator.comparing(p -> p.name);

        // Sorting by name
        people.sort(nameComparator);
        System.out.println("Sorted by name: " + people);

        // Comparator for sorting by age
        Comparator<Person> ageComparator = Comparator.comparingInt(p -> p.age);

        // Sorting by age
        people.sort(ageComparator);
        System.out.println("Sorted by age: " + people);
    }
}
```

### 19. Explain the Use of `Collections` Utility Class

The `Collections` utility class provides static methods that operate on or return collections. These include methods for sorting, searching, shuffling, and synchronizing collections.

**Code Snippet**:
```java
import java.util.*;

public class CollectionsUtilDemo {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>(Arrays.asList("C", "A", "B"));

        // Sorting
        Collections.sort(list);
        System.out.println("Sorted List: " + list);

        // Shuffling
        Collections.shuffle(list);
        System.out.println("Shuffled List: " + list);

        // Synchronizing
        List<String> syncList = Collections.synchronizedList(new ArrayList<>(list));
        System.out.println("Synchronized List: " + syncList);
    }
}
```

### 20. How Do You Clone a Collection?

You can clone a collection using the `clone()` method provided by the `Cloneable` interface, but it's important to note that not all collections support cloning or provide a deep copy.

**Code Snippet**:
```java
import java.util.*;

public class CloneDemo {
    public static void main(String[] args) {
        List<String> originalList = new ArrayList<>(Arrays.asList("A", "B", "C"));

        // Cloning using clone method
        @SuppressWarnings("unchecked")
        List<String> clonedList = (List<String>) ((ArrayList<String>) originalList).clone();
        
        System.out.println("Original List: " + originalList);
        System.out.println("Cloned List: " + clonedList);
    }
}
```

### 21. How Do You Convert an Array to a `List` and Vice Versa?

**Array to List**: You can use `Arrays.asList()` method to convert an array to a `List`.

**List to Array**: You can use the `toArray()` method of the `List` interface to convert a `List` to an array.

**Code Snippet**:
```java
import java.util.*;

public class ArrayListConversion {
    public static void main(String[] args) {
        // Array to List
        String[] array = {"One", "Two", "Three"};
        List<String> listFromArray = Arrays.asList(array);
        System.out.println("List from Array: " + listFromArray);

        // List to Array
        List<String> list = new ArrayList<>(Arrays.asList("Four", "Five", "Six"));
        String[] arrayFromList = list.toArray(new String[0]);
        System.out.println("Array from List: " + Arrays.toString(arrayFromList));
    }
}
```

### 22. Given a List of Integers, Find the Second Largest Element Efficiently

To find the second largest element efficiently, iterate through the list once, keeping track of the largest and second-largest elements.

**Code Snippet**:
```java
import java.util.*;

public class SecondLargestElement {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(10, 20, 4, 45, 99, 99, 12);

        Integer largest = null;
        Integer secondLargest = null;

        for (Integer number : numbers) {
            if (largest == null || number > largest) {
                secondLargest = largest;
                largest = number;
            } else if (number < largest && (secondLargest == null || number > secondLargest)) {
                secondLargest = number;
            }
        }

        System.out.println("Second Largest Element: " + secondLargest);
    }
}
```

### 23. How Would You Remove Duplicates from a `List`?

You can remove duplicates from a `List` by converting it to a `Set` and then back to a `List`.

**Code Snippet**:
```java
import java.util.*;

public class RemoveDuplicates {
    public static void main(String[] args) {
        List<String> listWithDuplicates = Arrays.asList("apple", "banana", "apple", "orange", "banana");

        // Removing duplicates
        Set<String> set = new HashSet<>(listWithDuplicates);
        List<String> listWithoutDuplicates = new ArrayList<>(set);

        System.out.println("List without duplicates: " + listWithoutDuplicates);
    }
}
```

### 24. How Would You Find the Most Frequent Element in a `List`?

To find the most frequent element, use a `Map` to count occurrences and then determine the element with the highest count.

**Code Snippet**:
```java
import java.util.*;

public class MostFrequentElement {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("apple", "banana", "apple", "orange", "banana", "banana");

        // Counting occurrences
        Map<String, Integer> frequencyMap = new HashMap<>();
        for (String item : list) {
            frequencyMap.put(item, frequencyMap.getOrDefault(item, 0) + 1);
        }

        // Finding the most frequent element
        String mostFrequent = null;
        int maxCount = 0;
        for (Map.Entry<String, Integer> entry : frequencyMap.entrySet()) {
            if (entry.getValue() > maxCount) {
                maxCount = entry.getValue();
                mostFrequent = entry.getKey();
            }
        }

        System.out.println("Most Frequent Element: " + mostFrequent);
    }
}
```

### 25. How Would You Implement an LRU Cache Using Java Collections?

An LRU (Least Recently Used) cache can be implemented using a combination of a `LinkedHashMap` and its access order feature. The `LinkedHashMap` maintains insertion order, but if you configure it to use access order, it will maintain the order of access.

**Code Snippet**:
```java
import java.util.*;

public class LRUCache<K, V> extends LinkedHashMap<K, V> {
    private final int capacity;

    public LRUCache(int capacity) {
        super(capacity, 0.75f, true); // Access order is true
        this.capacity = capacity;
    }

    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > capacity;
    }

    public static void main(String[] args) {
        LRUCache<Integer, String> lruCache = new LRUCache<>(3);

        lruCache.put(1, "One");
        lruCache.put(2, "Two");
        lruCache.put(3, "Three");
        System.out.println("LRU Cache: " + lruCache);

        lruCache.get(1); // Access key 1
        lruCache.put(4, "Four"); // This should evict key 2

        System.out.println("LRU Cache after eviction: " + lruCache);
    }
}
```