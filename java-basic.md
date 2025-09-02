### I. Core Java Concepts & OOP

1.  **Q: Explain the four fundamental principles of Object-Oriented Programming (OOP) in Java.**
    *   **A:**
        *   **Encapsulation:** Bundling data (attributes) and methods that operate on the data within a single unit (class) and restricting direct access to some of the object's components. Achieved using access modifiers (`private`, `protected`, `public`).
        *   **Inheritance:** A mechanism where one class (subclass/child) acquires the properties and behaviors of another class (superclass/parent). This promotes code reusability. Java supports single inheritance via `extends` keyword.
        *   **Polymorphism:** The ability of an object to take on many forms. In Java, it primarily refers to method overriding (runtime polymorphism) and method overloading (compile-time polymorphism).
        *   **Abstraction:** Hiding complex implementation details and showing only the essential features of an object. Achieved using abstract classes and interfaces.
2.  **Q: What is the difference between `interface` and `abstract class` in Java?**
    *   **A:**
        | Feature          | Interface                                   | Abstract Class                                 |
        | :--------------- | :------------------------------------------ | :--------------------------------------------- |
        | **Type**         | Pure abstraction blueprint                  | Partial abstraction blueprint                  |
        | **Methods**      | All methods are implicitly `public abstract` (before Java 8), can have `default` and `static` methods (Java 8+), `private` methods (Java 9+). | Can have abstract and non-abstract (concrete) methods. |
        | **Variables**    | All variables are implicitly `public static final`. | Can have `final`, `non-final`, `static`, `non-static` variables. |
        | **Constructors** | Cannot have constructors.                   | Can have constructors.                         |
        | **Inheritance**  | A class `implements` an interface. Can implement multiple interfaces. | A class `extends` an abstract class. Can extend only one abstract class. |
        | **Access**       | Members are implicitly `public`.            | Can have any access modifiers for members.     |
3.  **Q: Explain `final`, `finally`, and `finalize` in Java.**
    *   **A:**
        *   **`final` (keyword):** Used to restrict.
            *   `final` variable: Its value cannot be changed once initialized (becomes a constant).
            *   `final` method: Cannot be overridden by subclasses.
            *   `final` class: Cannot be subclassed (inherited).
        *   **`finally` (block):** A block of code associated with a `try-catch` block. It always executes, regardless of whether an exception occurred or was caught, making it ideal for cleanup code (e.g., closing resources).
        *   **`finalize` (method):** A method of the `Object` class, deprecated since Java 9. It was called by the Garbage Collector just before an object was reclaimed. Its execution is not guaranteed, and it's generally discouraged due to performance overhead and unpredictability.
4.  **Q: What is the `static` keyword used for in Java?**
    *   **A:** The `static` keyword indicates that a member (variable or method) belongs to the class itself, rather than to any specific instance of the class.
        *   **`static` variable:** A class variable, shared by all instances of the class. Only one copy exists.
        *   **`static` method:** Can be called directly using the class name, without creating an object. It can only access `static` members of the class.
        *   **`static` block:** Used to initialize `static` variables. Executes once when the class is loaded.
        *   **`static` nested class:** An inner class that can be instantiated without an outer class instance.
5.  **Q: Explain the difference between `String`, `StringBuilder`, and `StringBuffer`.**
    *   **A:**
        *   **`String`:** Immutable. Once a `String` object is created, its content cannot be changed. Any operation that appears to modify a `String` actually creates a new `String` object. Good for constant strings and when thread-safety is not a concern.
        *   **`StringBuffer`:** Mutable and Thread-safe. Its contents can be modified without creating new objects. All its methods are synchronized, making it suitable for multi-threaded environments where multiple threads might access the same string buffer.
        *   **`StringBuilder`:** Mutable and Non-thread-safe. Similar to `StringBuffer` in mutability, but its methods are not synchronized. This makes it faster than `StringBuffer` for single-threaded environments.
6.  **Q: What is the difference between `==` and `.equals()` in Java?**
    *   **A:**
        *   **`==` (operator):**
            *   For primitive types (e.g., `int`, `char`, `boolean`), it compares their actual values.
            *   For object types, it compares the memory addresses (references) of the objects. It checks if two object references point to the *exact same object* in memory.
        *   **`.equals()` (method):**
            *   A method defined in the `Object` class. By default, its behavior is the same as `==` (compares references).
            *   However, it is *overridden* in many classes (like `String`, `Integer`, `Date`, etc.) to compare the *content* or *state* of the objects rather than their memory addresses. You should always override `equals()` in your custom classes if you want to define equality based on object state.
7.  **Q: Why is it important to override both `equals()` and `hashCode()` methods together?**
    *   **A:** The contract between `equals()` and `hashCode()` states: "If two objects are equal according to the `equals(Object)` method, then calling the `hashCode()` method on each of the two objects must produce the same integer result."
        *   If you override `equals()` but not `hashCode()`, and two objects are `equal()` but have different `hashCode()` values, then collections that rely on hash codes (like `HashMap`, `HashSet`) will not work correctly. For example, a `HashSet` might store two equal objects because their hash codes differ, violating the set's uniqueness property.
        *   If `hashCode()` is overridden but `equals()` is not, then two objects with the same hash code might not be `equal()`, which is generally fine, but if `equals()` *should* return true for them, then you've violated the contract.

### II. Collections Framework

1.  **Q: Describe the Java Collections Framework hierarchy.**
    *   **A:** The core interfaces are:
        *   **`Iterable`:** The root interface for all collection classes. Enables iteration using enhanced for-loop.
        *   **`Collection`:** The root interface for all single-element collections. Extends `Iterable`.
            *   **`List`:** Ordered collection (sequence). Allows duplicate elements. Implementations: `ArrayList`, `LinkedList`, `Vector`.
            *   **`Set`:** Unordered collection. Does not allow duplicate elements. Implementations: `HashSet`, `LinkedHashSet`, `TreeSet`.
            *   **`Queue`:** Designed for holding elements prior to processing. Typically, FIFO (First-In, First-Out). Implementations: `PriorityQueue`, `ArrayDeque`.
        *   **`Map`:** A collection that maps keys to values. Keys must be unique. Implementations: `HashMap`, `LinkedHashMap`, `TreeMap`, `Hashtable`. (Note: `Map` does not extend `Collection`).
2.  **Q: Explain the differences between `ArrayList` and `LinkedList`.**
    *   **A:**
        *   **`ArrayList`:** Implements `List` interface using a dynamic array.
            *   **Access:** Fast random access (O(1)) because elements are stored contiguously in memory.
            *   **Insertion/Deletion:** Slow (O(n)) in the middle, as it requires shifting elements. Fast (O(1) amortized) at the end.
            *   **Memory:** More memory overhead for capacity management (resizing).
        *   **`LinkedList`:** Implements `List` and `Deque` interfaces using a doubly-linked list.
            *   **Access:** Slow random access (O(n)) as it requires traversing the list from the beginning or end.
            *   **Insertion/Deletion:** Fast (O(1)) once the position is found, as it only involves updating pointers.
            *   **Memory:** More memory overhead per element (stores previous and next pointers).
        *   **Use Cases:** Use `ArrayList` when frequent random access is needed. Use `LinkedList` when frequent insertions/delitions in the middle of the list are common.
3.  **Q: Differentiate between `HashMap`, `LinkedHashMap`, and `TreeMap`.**
    *   **A:** All implement the `Map` interface.
        *   **`HashMap`:**
            *   **Order:** No guaranteed order of elements.
            *   **Performance:** Provides constant-time performance (O(1)) for `get` and `put` operations on average, assuming a good hash function.
            *   **Nulls:** Allows one `null` key and multiple `null` values.
        *   **`LinkedHashMap`:**
            *   **Order:** Maintains insertion order (or access order, if configured). Iterating over the map yields elements in the order they were inserted.
            *   **Performance:** Slightly slower than `HashMap` due to the overhead of maintaining the linked list.
            *   **Nulls:** Allows one `null` key and multiple `null` values.
        *   **`TreeMap`:**
            *   **Order:** Stores elements in a natural sorting order of keys or by a custom `Comparator` provided at creation time.
            *   **Performance:** Provides guaranteed `log(n)` time cost for `get`, `put`, and `remove` operations.
            *   **Nulls:** Does not allow `null` keys (as it relies on comparison), but allows multiple `null` values.
        *   **Use Cases:** `HashMap` for general-purpose key-value storage. `LinkedHashMap` when insertion order matters. `TreeMap` when sorted order of keys is required.

### III. Exception Handling

1.  **Q: What is an exception in Java? Explain `checked` vs. `unchecked` exceptions.**
    *   **A:** An **exception** is an event that disrupts the normal flow of a program. It's an object that encapsulates an error condition.
        *   **`Checked` Exceptions:** These are exceptions that *must* be handled (either by `try-catch` block or by declaring `throws` in the method signature). The compiler enforces this handling. They typically represent predictable but unrecoverable problems (e.g., `IOException`, `SQLException`, `ClassNotFoundException`).
        *   **`Unchecked` Exceptions (Runtime Exceptions):** These are exceptions that do *not* need to be explicitly handled. They usually indicate programming errors (e.g., `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ArithmeticException`). The compiler does not enforce their handling, but they can still be caught.
2.  **Q: When would you use `throw` versus `throws`?**
    *   **A:**
        *   **`throw` (keyword):** Used *inside* a method body to explicitly throw an instance of an exception. You `throw` an exception object.
            ```java
            if (age < 0) {
                throw new IllegalArgumentException("Age cannot be negative");
            }
            ```
        *   **`throws` (keyword):** Used in a method signature to declare that a method *might* throw one or more checked exceptions. It's a way of telling the calling code that it needs to handle these potential exceptions.
            ```java
            public void readFile(String filePath) throws IOException {
                // ... code that might throw IOException
            }
            ```
3.  **Q: Can you have a `try` block without a `catch` block?**
    *   **A:** Yes, if it has a `finally` block. A `try-finally` block is valid and ensures the `finally` block executes regardless of whether an exception occurs in the `try` block. This is often used for resource cleanup.
    *   Also, with **try-with-resources** (Java 7+), you can have a `try` block without `catch` or `finally` if the resources declared in the `try` statement are auto-closable.
        ```java
        try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
            // ...
        } // No catch or finally needed if you don't want to handle the exception, it will propagate
        ```

### IV. Multithreading / Concurrency

1.  **Q: How can you create a thread in Java? What are the differences between the approaches?**
    *   **A:**
        *   **Extending the `Thread` class:**
            ```java
            class MyThread extends Thread {
                public void run() {
                    System.out.println("Thread using Thread class.");
                }
            }
            // To run: new MyThread().start();
            ```
            **Difference:** If you extend `Thread`, your class cannot extend any other class because Java does not support multiple inheritance.
        *   **Implementing the `Runnable` interface:**
            ```java
            class MyRunnable implements Runnable {
                public void run() {
                    System.out.println("Thread using Runnable interface.");
                }
            }
            // To run: new Thread(new MyRunnable()).start();
            ```
            **Difference:** This is generally preferred because it allows your class to extend another class while still enabling multithreading. It also separates the task (Runnable) from the thread execution mechanism (Thread).
2.  **Q: What is the `synchronized` keyword in Java?**
    *   **A:** The `synchronized` keyword is used to achieve thread safety. It can be applied to methods or blocks of code.
        *   When a method is `synchronized`, only one thread can execute that method on a given object instance at a time. The thread acquires a lock on the object.
        *   When a block of code is `synchronized` on an object, only one thread can execute that block at a time while holding the lock for that specific object.
        *   `synchronized` static methods acquire a lock on the class itself, not on an instance.
    *   It prevents data corruption in shared resources by ensuring that critical sections of code are executed by only one thread at a time.
3.  **Q: Explain `wait()`, `notify()`, and `notifyAll()`. What's important about them?**
    *   **A:** These methods are used for inter-thread communication and are defined in the `Object` class.
        *   **`wait()`:** Causes the current thread to release the lock it holds on an object and go into a waiting state until another thread invokes `notify()` or `notifyAll()` on the same object, or the specified timeout elapses. The thread must reacquire the lock before continuing execution.
        *   **`notify()`:** Wakes up a single thread that is waiting on this object's monitor (lock). If multiple threads are waiting, only one (arbitrarily chosen by JVM) will be awakened.
        *   **`notifyAll()`:** Wakes up all threads that are waiting on this object's monitor.
        *   **Important:**
            *   These methods *must* be called from within a `synchronized` block or method. If not, an `IllegalMonitorStateException` will be thrown.
            *   They are used to implement the Producer-Consumer pattern.
            *   They work on the intrinsic lock (monitor) of an object.

### V. JVM, JRE, JDK

1.  **Q: What is the difference between JVM, JRE, and JDK?**
    *   **A:**
        *   **JVM (Java Virtual Machine):** An abstract machine that provides a runtime environment in which Java bytecode can be executed. It's the core component that enables Java's "write once, run anywhere" capability. It interprets and executes the `.class` files.
        *   **JRE (Java Runtime Environment):** Includes the JVM, along with the core Java class libraries (like `java.lang`, `java.util`, `java.io`, etc.) and supporting files. It's what you need to *run* Java applications. It does not contain development tools like compilers.
        *   **JDK (Java Development Kit):** The complete software development kit. It includes the JRE, plus development tools such as the Java compiler (`javac`), debugger, archiving tool (`jar`), documentation generator (`javadoc`), etc. It's what you need to *develop* Java applications.

### VI. Other Important Concepts

1.  **Q: What is garbage collection in Java? How does it work?**
    *   **A:** Garbage collection (GC) is an automatic memory management process in Java. It automatically reclaims memory that is no longer being used by the program (i.e., objects that are no longer reachable or referenced by any part of the application).
    *   **How it works (simplified):** The JVM keeps track of all objects created. When an object is no longer referenced by any active part of the program, it becomes eligible for garbage collection. The GC then periodically identifies these unreachable objects and frees up the memory they occupied. Developers don't explicitly deallocate memory like in C++.
    *   **Benefits:** Reduces memory leaks, simplifies memory management for developers.
    *   **Drawbacks:** Can cause temporary pauses (stop-the-world events) in application execution during intensive GC cycles, though modern GCs are highly optimized.
2.  **Q: What is JDBC? Briefly explain its role.**
    *   **A:** JDBC stands for Java Database Connectivity. It's a Java API that provides a standard way for Java applications to connect to and interact with various relational databases (like MySQL, PostgreSQL, Oracle, SQL Server, etc.).
    *   **Role:** It defines a set of interfaces and classes that allow developers to:
        *   Establish a connection to a database.
        *   Send SQL queries (DML and DDL statements).
        *   Process the results returned by the database.
        *   Manage transactions.
    *   Database vendors provide specific JDBC drivers that implement these interfaces, allowing Java applications to be database-agnostic.
3.  **Q: What are Maven or Gradle? Why are they used?**
    *   **A:** Maven and Gradle are popular **build automation tools** for Java projects (and other languages).
        *   **Purpose:** They simplify and standardize the build process of software projects.
        *   **Key functionalities:**
            *   **Dependency Management:** Automatically download and manage project dependencies (libraries, frameworks).
            *   **Build Lifecycle:** Define phases like compile, test, package, install, deploy.
            *   **Project Structure:** Enforce a standard directory layout.
            *   **Reporting:** Generate various reports (e.g., test reports, code coverage).
            *   **Plugin Ecosystem:** Extend functionality with a wide range of plugins.
        *   **Difference:** Maven uses XML for configuration (`pom.xml`), while Gradle uses Groovy or Kotlin DSL for configuration (`build.gradle`), offering more flexibility and programmatic control.
4.  **Q: What is a Design Pattern? Can you give an example?**
    *   **A:** A Design Pattern is a general, reusable solution to a commonly occurring problem within a given context in software design. It's a template for how to solve a problem that can be used in many different situations. They are not finished designs that can be directly transformed into code, but rather descriptions or templates for how to solve a problem that can be used in many different situations.
    *   **Example (Singleton Pattern):**
        *   **Problem:** Ensure that a class has only one instance and provides a global point of access to it.
        *   **Solution:**
            *   Make the constructor `private` to prevent direct instantiation.
            *   Create a `static` method that returns the single instance of the class.
            *   Lazily initialize the instance within this `static` method (or eager initialization).
            *   Often used for logging, configuration managers, or thread pools.

### VII. Scenario-Based Questions

1.  **Q: You encounter a `NullPointerException` in your code. How do you debug and resolve it?**
    *   **A:**
        *   **Debugging:**
            1.  **Identify the line number:** The stack trace will point to the exact line where the `NPE` occurred.
            2.  **Examine the line:** Look for any variable that might be `null` when dereferenced (e.g., calling a method on a `null` object, accessing a field of a `null` object).
            3.  **Check variable values:** Use a debugger to inspect the values of variables leading up to that line.
            4.  **Trace back:** Understand why that specific variable became `null` (e.g., wasn't initialized, method returned `null` unexpectedly, incorrect logic).
        *   **Resolution:**
            1.  **Null Checks:** Add `if (variable != null)` checks before using the variable.
            2.  **Initialization:** Ensure variables are properly initialized before use.
            3.  **Defensive Programming:** Use `Optional` (Java 8+) for methods that might legitimately return `null` to force callers to handle the `null` case explicitly.
            4.  **Refactor:** If `null` indicates a logical error, fix the logic that leads to the `null` state.
            5.  **Fail Fast:** Throw an `IllegalArgumentException` or `NullPointerException` explicitly at an earlier stage if a `null` value is truly invalid input.
2.  **Q: You need to process a large file line by line without loading the entire file into memory. How would you do this in Java?**
    *   **A:** I would use `BufferedReader` for efficient reading of characters, combined with `FileReader`.
        ```java
        try (BufferedReader reader = new BufferedReader(new FileReader("large_file.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                // Process each 'line' here
                System.out.println(line);
            }
        } catch (IOException e) {
            System.err.println("Error reading file: " + e.getMessage());
        }
        ```
        *   **Explanation:** `BufferedReader` reads characters into a buffer, which makes reading line by line much more efficient than reading single characters. `readLine()` returns `null` when the end of the stream is reached. The try-with-resources statement ensures that the `BufferedReader` (and underlying `FileReader`) is automatically closed, even if an exception occurs.
3.  **Q: Your application is experiencing slow performance. What are some common areas you would investigate in a Java application?**
    *   **A:**
        1.  **CPU Usage:**
            *   **Infinite Loops/Tight Loops:** Code that consumes CPU without making progress.
            *   **Inefficient Algorithms:** Using O($$N^2$$) where O(N) or O($$logN$$) is possible.
            *   **Excessive Object Creation:** Leading to frequent and costly Garbage Collection.
        2.  **Memory Usage:**
            *   **Memory Leaks:** Objects are retained longer than needed, leading to `OutOfMemoryError`.
            *   **High GC Activity:** Frequent or long "stop-the-world" pauses due to large heap or inefficient GC configuration.
            *   **Large Data Structures:** Holding too much data in memory.
        3.  **I/O Operations:**
            *   **Disk I/O:** Slow file reads/writes.
            *   **Network I/O:** Latency or bandwidth issues with external services (databases, APIs, message queues).
            *   **Database Queries:** Inefficient SQL queries, missing indexes, large result sets.
        4.  **Concurrency Issues:**
            *   **Thread Contention/Locking:** Too many threads trying to acquire the same lock, leading to serialization and reduced parallelism.
            *   **Deadlocks:** Threads waiting indefinitely for each other.
            *   **Under-utilization:** Not enough threads, or threads spending too much time waiting.
        5.  **External Dependencies:**
            *   Slow response times from external APIs, databases, or message brokers.
        6.  **Logging:** Excessive or synchronous logging can introduce overhead.
        7.  **Configuration:** Suboptimal JVM arguments (heap size, GC algorithm), connection pool sizes, etc.
