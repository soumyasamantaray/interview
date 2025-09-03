Here are brief answers to your questions:

1.  **Difference between Memory and JVM**
    *   **Memory:** Refers to the physical RAM of the computer.
    *   **JVM (Java Virtual Machine):** A software layer that runs on the operating system and uses a portion of the physical memory. The JVM manages its own memory areas (Heap, Stack, Method Area/Metaspace, PC Registers) within the allocated physical memory.

2.  **Difference between ArrayList and LinkedList**
    *   **ArrayList:** Implemented using a dynamic array.
        *   **Pros:** Fast random access ($$O(1)$$), good for retrieving elements.
        *   **Cons:** Slower insertions/deletions in the middle ($$O(n)$$ as elements need to be shifted).
    *   **LinkedList:** Implemented using a doubly linked list.
        *   **Pros:** Fast insertions/deletions at any position ($$O(1)$$ once the position is found, $$O(n)$$ to find it if not at ends).
        *   **Cons:** Slower random access ($$O(n)$$ as it needs to traverse from the beginning or end).

3.  **Write the programming for custom ArrayList**
    *   A custom `ArrayList` would internally use a `private Object[] elements;` array and a `private int size;`.
    *   The core logic involves:
        *   `add(E e)`: Adds an element. If the array is full, it resizes by creating a new, larger array and copying existing elements.
        *   `get(int index)`: Returns the element at `index`, with bounds checking.
        *   `remove(int index)`: Removes an element, shifts subsequent elements, and potentially shrinks the array.

    ```java
    import java.util.Arrays;

    public class CustomArrayList<E> {
        private Object[] elements;
        private int size;
        private static final int DEFAULT_CAPACITY = 10;

        public CustomArrayList() {
            elements = new Object[DEFAULT_CAPACITY];
            size = 0;
        }

        public void add(E e) {
            if (size == elements.length) {
                // Double the capacity
                Object[] newElements = new Object[elements.length * 2];
                System.arraycopy(elements, 0, newElements, 0, size);
                elements = newElements;
            }
            elements[size++] = e;
        }

        public E get(int i) {
            if (i >= size || i < 0) {
                throw new IndexOutOfBoundsException("Index: " + i + ", Size: " + size);
            }
            return (E) elements[i];
        }

        public boolean remove(Object o) {
            for (int i = 0; i < size; i++) {
                if (o.equals(elements[i])) {
                    remove(i);
                    return true;
                }
            }
            return false;
        }

        public E remove(int index) {
            if (index >= size || index < 0) {
                throw new IndexOutOfBoundsException("Index: " + index + ", Size: " + size);
            }
            E oldValue = (E) elements[index];
            int numMoved = size - index - 1;
            if (numMoved > 0) {
                System.arraycopy(elements, index + 1, elements, index, numMoved);
            }
            elements[--size] = null; // Clear to let GC do its work
            return oldValue;
        }

        public int size() {
            return size;
        }

        public boolean isEmpty() {
            return size == 0;
        }

        @Override
        public String toString() {
            return Arrays.toString(Arrays.copyOf(elements, size));
        }

        // Example usage:
        public static void main(String[] args) {
            CustomArrayList<String> list = new CustomArrayList<>();
            list.add("Apple");
            list.add("Banana");
            list.add("Cherry");
            System.out.println("List: " + list); // List: [Apple, Banana, Cherry]
            System.out.println("Size: " + list.size()); // Size: 3
            System.out.println("Get at index 1: " + list.get(1)); // Get at index 1: Banana
            list.remove(0);
            System.out.println("List after removing index 0: " + list); // List after removing index 0: [Banana, Cherry]
            list.add("Date");
            System.out.println("List after adding Date: " + list); // List after adding Date: [Banana, Cherry, Date]
        }
    }
    ```

4.  **How the HashMap is working internally as per below Java 8 and Java 8 versions**
    *   **Pre-Java 8:** `HashMap` used an array of `LinkedList`s (buckets). When a hash collision occurred (two keys mapped to the same bucket index), the new entry was simply added to the `LinkedList` at that index. Retrieval involved iterating through the `LinkedList`. Worst-case performance for lookups, insertions, deletions was $$O(n)$$ if all elements ended up in one `LinkedList`.
    *   **Java 8 and later:** Still uses an array of buckets. However, to improve performance for high collision rates, if a `LinkedList` in a bucket exceeds a certain threshold (default 8 nodes), it converts that `LinkedList` into a balanced **Red-Black Tree**. This changes the worst-case performance for lookups, insertions, deletions from $$O(n)$$ to $$O(\log n)$$. If the number of nodes in the tree falls below a certain threshold (default 6), it converts back to a `LinkedList`.

5.  **What is thread-safe?**
    *   **Thread-safe:** Code or data structures are thread-safe if they can be executed or accessed by multiple threads concurrently without causing data corruption, inconsistent results, or deadlocks. This typically involves mechanisms like synchronization, locks, or using immutable objects.

6.  **Difference between Volatile and Synchronized keyword**
    *   **`volatile` keyword:**
        *   **Visibility:** Ensures that changes to a `volatile` variable are immediately written to main memory and read from main memory by all threads.
        *   **Atomicity:** Does not guarantee atomicity for operations involving multiple steps (e.g., `i++`).
        *   **Mutual Exclusion:** Does not provide mutual exclusion; multiple threads can access a `volatile` variable concurrently.
    *   **`synchronized` keyword:**
        *   **Visibility:** Ensures visibility of changes (happens-before guarantee) by flushing writes to main memory before releasing a lock and re-reading from main memory after acquiring a lock.
        *   **Atomicity:** Ensures atomicity for the code block or method it encloses.
        *   **Mutual Exclusion:** Provides mutual exclusion; only one thread can execute a `synchronized` block/method on a given object (or class for static methods) at a time.

7.  **Explain about String and String literals**
    *   **`String`:** In Java, `String` is a class that represents sequences of characters. `String` objects are **immutable**, meaning once a `String` object is created, its content cannot be changed. Any operation that seems to modify a `String` (like `concat()`) actually creates a new `String` object.
    *   **String Literals:** These are `String` values enclosed in double quotes (e.g., `"hello"`). Java optimizes `String` literals by storing them in a special memory area called the **String Pool** (part of the heap, formerly PermGen/Metaspace). If a literal already exists in the pool, a reference to the existing object is returned instead of creating a new one, saving memory and improving performance.

8.  **Write a programming for custom Immutable class**
    *   To make a class immutable:
        1.  Declare the class as `final` (prevents subclassing).
        2.  Declare all fields as `private` and `final`.
        3.  Do not provide any setter methods for fields.
        4.  Initialize all fields through the constructor.
        5.  For any mutable object fields (e.g., `List`, `Date`), perform a deep copy in the constructor and return a deep copy in the getter to prevent external modification.

    ```java
    import java.util.ArrayList;
    import java.util.List;
    import java.util.Collections; // For unmodifiable list example

    public final class ImmutablePerson { // 1. Final class
        private final String name;       // 2. Final fields
        private final int age;
        private final List<String> hobbies; // Mutable field

        public ImmutablePerson(String name, int age, List<String> hobbies) {
            this.name = name;
            this.age = age;
            // 5. Deep copy mutable objects in constructor
            // Option A: New ArrayList (recommended for common use)
            this.hobbies = new ArrayList<>(hobbies);
            // Option B: Unmodifiable List (if you don't need to modify internally later)
            // this.hobbies = Collections.unmodifiableList(new ArrayList<>(hobbies));
        }

        public String getName() {
            return name;
        }

        public int getAge() {
            return age;
        }

        public List<String> getHobbies() {
            // 5. Return a deep copy of mutable objects in getters
            return new ArrayList<>(hobbies);
            // If hobbies was created with Collections.unmodifiableList:
            // return hobbies; // This is safe because the list itself is unmodifiable
        }

        // No setter methods
        // No methods that modify the state of the object after construction
    }
    ```

9.  **What’s the importance of hashCode() and equals() method**
    *   **Importance:** They are fundamental for correct behavior of objects in Java collections, especially `HashMap`, `HashSet`, and `Hashtable`.
    *   **`equals()`:** Defines logical equality between objects. If two objects are considered "equal" based on business logic, `equals()` should return `true`.
    *   **`hashCode()`:** Returns an integer hash code for an object. It's used by hash-based collections to quickly determine the initial bucket where an object *might* be located.
    *   **Contract:**
        1.  If two objects are equal according to the `equals(Object)` method, then calling the `hashCode` method on each of the two objects must produce the same integer result.
        2.  If two objects are unequal according to the `equals(Object)` method, it is *not* required that calling the `hashCode` method on each of the two objects must produce distinct integer results. However, distinct hash codes for unequal objects can improve collection performance.
    *   **Why both?** If you override `equals()` but not `hashCode()`, equal objects might produce different hash codes. This would cause `HashSet` to store both objects (violating set uniqueness) or `HashMap` to fail to find a value associated with a key, as they would be placed in different buckets.

10. **What’s the difference between map and flatMap in stream api**
    *   **`map()`:** Performs a one-to-one transformation on elements in a stream. It takes a `Function` that returns a single value for each input element. The resulting stream has the same number of elements as the input stream.
        *   Example: `Stream<String> -> Stream<Integer>` (e.g., converting strings to their lengths).
        ```java
        List<String> words = Arrays.asList("hello", "world");
        List<Integer> lengths = words.stream()
                                     .map(String::length) // Transforms each String to its length
                                     .collect(Collectors.toList()); //
        ```
    *   **`flatMap()`:** Performs a one-to-many transformation and then "flattens" the resulting streams into a single stream. It takes a `Function` that returns a `Stream` for each input element. The individual streams are then concatenated. Useful when you have a stream of collections (or something that can produce multiple elements) and you want to process all elements *within* those collections as a single flat stream.
        *   Example: `Stream<List<String>> -> Stream<String>` (e.g., combining lists of words into a single stream of words).
        ```java
        List<List<String>> sentences = Arrays.asList(
            Arrays.asList("Java", "Stream"),
            Arrays.asList("API", "Example")
        );
        List<String> allWords = sentences.stream()
                                         .flatMap(Collection::stream) // Transforms each List<String> to a Stream<String> and flattens
                                         .collect(Collectors.toList()); // [Java, Stream, API, Example]
        ```

11. **What is lambda expression and how it’s working?**
    *   **Lambda Expression:** An anonymous function that provides a concise way to implement an interface with a single abstract method (a "functional interface"). It allows you to treat functionality as a method argument or code as data.
        *   Syntax: `(parameters) -> expression` or `(parameters) -> { statements; }`
        *   Example: `(a, b) -> a + b` (for an interface like `IntBinaryOperator`).
        ```java
        // Using a lambda for a functional interface (e.g., Runnable)
        Runnable myRunnable = () -> System.out.println("Hello from lambda!");
        new Thread(myRunnable).start();

        // Using a lambda with Stream API
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4);
        numbers.forEach(n -> System.out.println(n * 2)); // Prints 2, 4, 6, 8
        ```
    *   **How it's working:** At compile time, the Java compiler translates lambda expressions into instances of the corresponding functional interface. Internally, it typically uses the `invokedynamic` instruction and `MethodHandles` to generate the necessary bytecode at runtime, rather than creating an anonymous inner class for every lambda (though it can sometimes optimize to that). This makes lambdas more efficient and flexible than anonymous inner classes.

12. **How the garbage collector will work.**
    *   **Purpose:** The Garbage Collector (GC) is a daemon process in the JVM that automatically reclaims memory occupied by objects that are no longer reachable (referenced) by the running application. This frees up developers from manual memory management.
    *   **Working (Simplified):**
        1.  **Marking:** The GC identifies all reachable objects starting from "GC roots" (e.g., local variables on the stack, static fields). Objects not marked as reachable are considered garbage.
        2.  **Sweeping:** The GC reclaims the memory occupied by the unmarked (unreachable) objects.
        3.  **Compacting (Optional):** After sweeping, memory can become fragmented. Some GCs perform compaction to defragment the heap by moving reachable objects closer together, making larger contiguous blocks of free memory available.
    *   **Generational GC:** Most modern GCs use a generational approach:
        *   **Young Generation:** Where new objects are initially allocated. Most objects die young. Uses a fast copying algorithm.
        *   **Old Generation (Tenured):** Objects that survive multiple garbage collection cycles in the Young Generation are promoted here. GC cycles here are less frequent but can be longer.
        *   **Metaspace (formerly Permanent Generation):** Stores metadata about classes and methods.

13. **What is class loader and how its working?**
    *   **Class Loader:** A component of the Java Virtual Machine (JVM) that is responsible for dynamically loading Java classes (`.class` files) into the JVM's memory during runtime.
    *   **How it's working (Delegation Model):**
        1.  **Loading:** Finds the `.class` file for a given class name (e.g., from classpath, JARs, network).
        2.  **Linking:**
            *   **Verification:** Ensures the loaded bytecode is structurally correct and safe.
            *   **Preparation:** Allocates memory for static fields and initializes them to default values.
            *   **Resolution (Optional):** Replaces symbolic references in the code (e.g., to other classes or methods) with direct references.
        3.  **Initialization:** Executes the static initializers and static blocks of the class.
    *   **Hierarchy/Delegation:** Class loaders operate in a hierarchical manner:
        *   **Bootstrap Class Loader:** Built into the JVM, loads core Java API classes (from `rt.jar` or equivalent).
        *   **Extension Class Loader:** Loads classes from the Java extensions directory (`jre/lib/ext`).
        *   **Application (System) Class Loader:** Loads classes from your application's classpath.
        When a class needs to be loaded, the request is first delegated upwards to the parent class loader. Only if the parent cannot find or load the class will the current class loader attempt to load it. This prevents duplicate class loading and ensures core Java classes are always loaded by the Bootstrap loader.
