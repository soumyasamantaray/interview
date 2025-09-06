# 5-Day Java Interview Preparation Guide

This guide provides a structured 5-day plan to prepare for Java interviews, covering core concepts, advanced topics, and common interview questions.

## Table of Contents

*   [📅 Day 1: Core Java & OOP Fundamentals](#-day-1-core-java--oop-fundamentals)
*   [📅 Day 2: Collections Framework & Exception Handling](#-day-2-collections-framework--exception-handling)
*   [📅 Day 3: Multithreading & Concurrency](#-day-3-multithreading--concurrency)
*   [📅 Day 4: Java 8+ Features & Design Patterns](#-day-4-java-8-features--design-patterns)
*   [📅 Day 5: Advanced Topics & Mock Interviews](#-day-5-advanced-topics--mock-interviews)
*   [🎯 Bonus: Must-Know Interview Questions](#-bonus-must-know-interview-questions)
*   [🚀 Final Advice](#-final-advice)

---

## 📅 Day 1: Core Java & OOP Fundamentals

### Topics to Cover:

#### 1. Java Basics

*   JDK vs JRE vs JVM
*   Platform independence & bytecode
*   `public static void main(String[] args)` breakdown
*   Primitive vs reference types

#### Questions and Answers:

*   **1. Difference between JDK, JRE, and JVM**

| Feature              | JDK (Java Development Kit)                               | JRE (Java Runtime Environment)                               | JVM (Java Virtual Machine)                                       |
| :------------------- | :------------------------------------------------------- | :----------------------------------------------------------- | :--------------------------------------------------------------- |
| **Purpose**          | Used to develop Java applications                        | Used to run Java applications                                | Runs Java bytecode                                               |
| **Contains**         | JRE + Development tools (compiler `javac`, debugger, etc.) | JVM + libraries + classes for runtime                        | Converts bytecode to machine code                                |
| **Includes**         | JRE + tools like `javac`, `javadoc`, etc.                | JVM + core Java class libraries                              | Just the virtual machine                                         |
| **User**             | Developers                                               | End-users                                                    | Internal component of JRE                                        |
| **Can compile code?** | ✅ Yes                                                   | ❌ No                                                        | ❌ No                                                            |

*   **2. Why is JVM called a Virtual Machine?**
    *   JVM is called a Virtual Machine because it simulates a machine (computer) that runs Java bytecode.
    *   It abstracts away the underlying hardware and operating system, allowing the same Java bytecode to run on any machine that has a JVM.
    *   It's "virtual" because it doesn't physically exist—it is a software-based engine that behaves like a real computer executing bytecode.

*   **3. Is JVM Platform Independent?**
    *   JVM itself is **NOT** platform-independent — each operating system has its own implementation of the JVM.
    *   However, Java bytecode is platform-independent, and the JVM makes Java platform-independent by allowing the same bytecode to run on different platforms.
    *   **Write Once, Run Anywhere (WORA)** is possible because the compiled bytecode can run on any JVM, regardless of the OS.

*   **4. Can you run a Java program without JDK?**
    *   ✅ Yes, you can run Java programs with only the JRE, but you cannot compile them.
    *   If you have a `.class` file (already compiled), you can use JRE (which includes JVM) to run it.
    *   ❌ You cannot compile `.java` files without the JDK because the compiler `javac` is part of the JDK.

*   **5. What happens when you compile a `.java` file?**
    1.  Compiler (`javac`) converts the `.java` file into a `.class` file.
    2.  This `.class` file contains **bytecode**, not machine code.
    3.  Bytecode is a platform-independent intermediate code that runs on the JVM.
    4.  When you run the `.class` file:
        *   JVM loads the bytecode.
        *   The ClassLoader loads classes.
        *   Bytecode Verifier checks for security and correctness.
        *   JIT (Just-In-Time) compiler converts bytecode to machine code at runtime.
        *   CPU executes the native code.

*   **How does Java achieve platform independence?**
    *   By compiling Java source code into platform-independent bytecode, which can then be executed by a platform-specific JVM.

*   **What is bytecode?**
    *   Bytecode is a set of instructions for the JVM, an intermediate representation of Java source code that is platform-independent.

*   **Can we see bytecode?**
    *   Yes, you can disassemble a `.class` file using the `javap` command-line tool (e.g., `javap -c MyClass.class`).

*   **Is bytecode OS-dependent?**
    *   No, bytecode is platform-independent. It's the JVM that is OS-dependent.

*   **Why not compile Java directly to machine code?**
    *   Compiling directly to machine code would sacrifice platform independence, requiring different executables for each operating system. Bytecode enables WORA.

*   **Why is the `main` method static?**
    *   Because the JVM needs to call the `main` method without creating an object of the class. If it weren't static, an object would need to be instantiated first, leading to a chicken-and-egg problem.

*   **Can the `main` method be private?**
    *   No, the `main` method must be `public` for the JVM to access and execute it.

*   **What if I write `String args[]` instead of `String[] args`?**
    *   Both are syntactically correct in Java. `String[] args` is generally preferred for consistency and clarity as it clearly indicates `args` is an array of `String` objects.

*   **Can we overload the `main()` method?**
    *   Yes, you can overload the `main()` method, but the JVM will only execute the one with the signature `public static void main(String[] args)`.

*   **What happens if the `main` method is missing?**
    *   The Java Virtual Machine will throw a `NoSuchMethodError` or similar error at runtime, as it won't find the entry point for execution.

*   **Difference between primitive and reference types?**
    *   **Primitive types** (e.g., `int`, `char`, `boolean`) store the actual value directly in memory.
    *   **Reference types** (e.g., `String`, `Object`, arrays) store references (memory addresses) to objects in the heap.

*   **Why Java is not 100% object-oriented?**
    *   Because it includes primitive data types (like `int`, `char`, `boolean`) which are not objects. While it provides wrapper classes for these, their existence means Java is not purely object-oriented.

*   **What is autoboxing and unboxing?**
    *   **Autoboxing:** Automatic conversion of a primitive type to its corresponding wrapper class (e.g., `int` to `Integer`).
    *   **Unboxing:** Automatic conversion of a wrapper class object to its corresponding primitive type (e.g., `Integer` to `int`).

*   **What is default value of `char` and `boolean`?**
    *   `char`: `\u0000` (null character)
    *   `boolean`: `false`

*   **Why does `char` take 2 bytes in Java?**
    *   To support Unicode characters, which require more than 1 byte to represent the broader range of international characters.

| Question                                    | Answer/Trick                                                      |
| :------------------------------------------ | :---------------------------------------------------------------- |
| **Can you run a Java class without `main()`?** | Yes, using static blocks (but not recommended in modern Java)     |
| **Is `String` a primitive type?**           | No, it's a reference type (class)                                 |
| **Is `null` a keyword?**                    | Yes                                                               |
| **Does JVM exist for each OS?**             | Yes, it’s platform-specific                                       |
| **What is the output of: `System.out.println(10 + 20 + "Java")`?** | `30Java` – because `10+20` is evaluated first (left-to-right precedence) |

#### 2. OOP Concepts

*   **4 Pillars of OOP** (Encapsulation, Inheritance, Polymorphism, Abstraction)
*   Difference between **Abstract Class vs Interface**
*   **Method Overloading vs Overriding**
*   **`final`, `finally`, `finalize`** differences
*   **`super` vs `this`** keyword

#### Questions and Answers:

*   **What is encapsulation and how is it implemented?**
    *   **Encapsulation** is the bundling of data (attributes) and methods that operate on the data into a single unit (class), and restricting direct access to some of the object's components.
    *   It's implemented using **access modifiers** (`private`, `protected`, `public`) and providing public **getter and setter methods** to access and modify private data.

*   **How is it different from abstraction?**
    *   **Encapsulation** is about *how* an object is implemented (hiding internal state and behavior).
    *   **Abstraction** is about *what* an object does (showing only essential features and hiding complex implementation details). You can achieve abstraction using abstract classes and interfaces.

*   **What type of inheritance is not supported in Java and why?**
    *   **Multiple inheritance of classes** is not supported in Java to avoid the "Diamond Problem," which can lead to ambiguity about which superclass method to inherit if multiple superclasses have methods with the same signature.

*   **Can constructors be inherited?**
    *   No, constructors are not inherited. A subclass can call a superclass's constructor using `super()`, but it doesn't inherit the constructor itself.

*   **Difference between overloading and overriding?**

| Feature     | Method Overloading                                     | Method Overriding                                           |
| :---------- | :----------------------------------------------------- | :---------------------------------------------------------- |
| **Definition** | Same method name, different parameters (signature)     | Same method name, same parameters (signature) as superclass |
| **Location** | Within the same class                                  | In a subclass (IS-A relationship)                           |
| **Resolution** | Compile-time (static polymorphism)                     | Run-time (dynamic polymorphism)                             |
| **Return Type** | Can be different                                       | Must be same or a covariant return type                     |
| **Access Modifier** | Can be different                                       | Cannot be more restrictive than superclass                  |

*   **Can we override a static method?**
    *   No, static methods cannot be overridden. If a subclass declares a static method with the same signature as a static method in its superclass, it's called "method hiding," not overriding.

*   **What is abstraction?**
    *   Abstraction is the process of hiding the implementation details and showing only the functionality to the user. It focuses on "what" the object does rather than "how" it does it.

*   **Which is better for abstraction: interface or abstract class?**
    *   It depends on the scenario:
        *   **Interface:** Better for defining contracts or capabilities that multiple, unrelated classes might implement. It achieves **100% abstraction** (prior to Java 8 default methods).
        *   **Abstract Class:** Better for providing a common base for related classes, allowing some methods to be implemented and others to be abstract. It offers **partial abstraction**.

*   **When to use abstract class vs interface?**
    *   **Abstract Class:** Use when you want to provide a common base implementation for subclasses, share code, and allow for some default behavior. Suitable for "is-a" relationships where classes share a common type and some implementation.
    *   **Interface:** Use when you want to define a contract or a set of behaviors that a class *can do*. Suitable for "can-do" or "has-a" relationships, or when multiple inheritance of behavior is needed.

*   **Can interface have a constructor?**
    *   No, interfaces cannot have constructors because they cannot be instantiated.

*   **Can we declare variables in interface?**
    *   Yes, but all variables declared in an interface are implicitly `public static final`. They are constants.

*   **Can a `final` method be overridden?**
    *   No, a `final` method cannot be overridden by subclasses. It's designed to prevent modification of its behavior.

*   **What is the use of `finally` block if exception occurs?**
    *   The `finally` block is used to execute code that *must* run, regardless of whether an exception occurred or was caught in the `try` block. It's typically used for cleanup operations like closing resources (file streams, database connections).

*   **Is `finalize()` guaranteed to execute?**
    *   No, `finalize()` is not guaranteed to execute. It's called by the garbage collector just before an object is garbage collected, but the timing and execution are unpredictable and dependent on the GC's schedule. It's deprecated in modern Java versions (replaced by `Cleaner`).

*   **Can we overload `finalize()`?**
    *   Yes, you can overload `finalize()` but only the one with no arguments (`protected void finalize()`) will be called by the garbage collector.

#### 3. String Handling

*   Why **String is immutable**?
*   **String vs StringBuilder vs StringBuffer**
*   **String Pool concept**

#### Questions and Answers:

*   **Why String is immutable?**
    *   **Security:** Used in class loading, file system operations, and network connections. Immutability prevents malicious code from altering a `String` reference, which could change the meaning of a path or URL.
    *   **Thread Safety:** Immutable objects are inherently thread-safe because their state cannot be changed once created. No synchronization is needed.
    *   **Performance:** Immutability allows `String` objects to be cached in the String Pool, saving memory and improving performance for frequently used strings. It also enables optimizations like hash code caching.
    *   **Caching:** The hash code of a `String` is frequently used in `HashMap` and `HashSet`. If `String` were mutable, its hash code could change, breaking these collections.

*   **String vs StringBuilder vs StringBuffer**

| Feature       | `String`                                  | `StringBuilder`                             | `StringBuffer`                                 |
| :------------ | :---------------------------------------- | :------------------------------------------ | :--------------------------------------------- |
| **Mutability** | Immutable                                 | Mutable                                     | Mutable                                        |
| **Thread-Safe** | Yes (inherently)                          | No (not synchronized)                       | Yes (synchronized)                             |
| **Performance** | Poor for concatenation (creates new objects) | Best for concatenation (no new objects)     | Good for concatenation (but slower than `StringBuilder` due to synchronization overhead) |
| **Usage**     | When string content is fixed              | When string content changes frequently in a single-threaded environment | When string content changes frequently in a multi-threaded environment |
| **Introduced** | Java 1.0                                  | Java 5                                      | Java 1.0                                       |

*   **String Pool concept**
    *   The String Pool (or String Intern Pool) is a special memory area within the Java Heap (specifically, within the Permanent Generation or Metaspace in newer JVMs) where `String` literals are stored.
    *   When a `String` literal is created (e.g., `String s = "hello";`), the JVM first checks the String Pool. If a `String` with the same content already exists, a reference to the existing object is returned. Otherwise, a new `String` object is created in the pool and a reference to it is returned.
    *   This mechanism saves memory by preventing duplicate `String` objects for identical literal values. The `intern()` method can be used to explicitly add a `String` object to the pool or get a reference from it.

### Practice Questions:

*   **What is the output of `"Hello" == new String("Hello")`?**
    *   `false`.
    *   `"Hello"` (literal) creates an object in the String Pool.
    *   `new String("Hello")` creates a new object in the heap (outside the pool).
    *   `==` compares references, and they point to different memory locations.

*   **Can we override a private/static method?**
    *   No.
        *   **Private methods** cannot be overridden because they are not visible outside their class.
        *   **Static methods** cannot be overridden; if a subclass has a static method with the same signature, it's "method hiding," not overriding.

*   **Why is Java not 100% object-oriented?**
    *   Because it supports primitive data types (e.g., `int`, `boolean`, `char`) which are not objects.

---

## 📅 Day 2: Collections Framework & Exception Handling

### Topics to Cover:

#### 1. Collections Framework

*   **List (ArrayList vs LinkedList)**
*   **Set (HashSet vs TreeSet vs LinkedHashSet)**
*   **Map (HashMap vs TreeMap vs LinkedHashMap)**
*   **Internal working of HashMap** (Hashing, Buckets, Collision, Load Factor)
*   **Fail-fast vs Fail-safe iterators**
*   **Comparable vs Comparator**

#### 2. Exception Handling

*   **Checked vs Unchecked Exceptions**
*   **`try-catch-finally` vs `try-with-resources`**
*   **Custom Exceptions**

### Practice Questions:

*   **Why does `HashMap` allow one `null` key?**
    *   `HashMap` allows one `null` key because it handles `null` specifically. The hash code for a `null` key is always `0`, so it always maps to the first bucket (`bucket[0]`). This allows `HashMap` to store one `null` key-value pair without needing a hash calculation.

*   **What happens if we don’t override `equals()` and `hashCode()`?**
    *   If you don't override `equals()` and `hashCode()` for a custom object used as a key in `HashMap` or an element in `HashSet`:
        *   `equals()` will use the default `Object` class implementation, which compares object references (`==`). This means two distinct objects with the same content will be considered unequal.
        *   `hashCode()` will return a unique integer for each object based on its memory address.
        *   As a result, `HashMap` and `HashSet` will treat two logically equal but distinct objects as different, leading to incorrect behavior (e.g., duplicate entries in a `HashSet`, or failing to retrieve a value from a `HashMap` using a logically identical but different key object).

*   **Difference between `throw` and `throws`?**

| Feature     | `throw`                                       | `throws`                                                    |
| :---------- | :-------------------------------------------- | :---------------------------------------------------------- |
| **Usage**   | Used to explicitly throw an exception object  | Used in a method signature to declare exceptions it might throw |
| **Keyword** | Followed by an instance of `Throwable`        | Followed by a class name of an exception                    |
| **Purpose** | To raise an exception                           | To inform the caller about potential exceptions             |
| **Placement** | Inside a method or block (`try-catch`)        | In the method signature                                     |
| **Effect**  | Immediate termination of current execution    | No immediate effect; just a declaration                     |

---

## 📅 Day 3: Multithreading & Concurrency

### Topics to Cover:

#### 1. Thread Basics

*   **Ways to create a thread** (`extends Thread` vs `implements Runnable` vs `Callable`)
*   **Thread Lifecycle** (New, Runnable, Blocked, Waiting, Terminated)

#### 2. Synchronization & Locks

*   **`synchronized` keyword** (method vs block)
*   **`volatile` keyword**
*   **Deadlock & Prevention**

#### 3. Concurrency Utilities

*   **ThreadPool & ExecutorService**
*   **`ConcurrentHashMap` vs `HashMap`**
*   **`CountDownLatch`, `CyclicBarrier`, `Semaphore`**

### Practice Questions:

*   **How to avoid deadlock in Java?**
    *   **Avoid Nested Locks:** Don't acquire a second lock if you already hold one.
    *   **Ordered Lock Acquisition:** Acquire locks in a predefined, consistent order across all threads.
    *   **Timeout for Locks:** Use `tryLock()` with a timeout to avoid indefinite waiting.
    *   **Resource Pre-allocation:** Acquire all necessary resources before starting the task.
    *   **Interruptible Locks:** Use `ReentrantLock.lockInterruptibly()` which allows a thread to be interrupted while waiting for a lock.

*   **Difference between `sleep()` and `wait()`?**

| Feature     | `sleep()`                                   | `wait()`                                                    |
| :---------- | :------------------------------------------ | :---------------------------------------------------------- |
| **Class**   | `Thread` class                              | `Object` class                                              |
| **Monitor Lock** | Does not release the monitor lock           | Releases the monitor lock                                   |
| **Usage**   | To pause execution for a specified duration | To make a thread wait until another thread notifies it      |
| **Context** | Can be called without `synchronized` block  | Must be called from a `synchronized` block/method           |
| **Wake-up** | Wakes up automatically after time expires   | Wakes up when `notify()` or `notifyAll()` is called, or timeout expires |
| **Static?** | `Thread.sleep()` is static                  | `wait()` is an instance method of `Object`                  |

*   **What is the `ThreadLocal` class?**
    *   `ThreadLocal` provides thread-local variables. Each thread that accesses a `ThreadLocal` variable has its own independent copy of the variable, initialized to a value. This allows threads to store and retrieve data without needing explicit synchronization, as each thread operates on its own isolated copy. It's useful for scenarios like storing user session data or transaction IDs per thread.

---

## 📅 Day 4: Java 8+ Features & Design Patterns

### Topics to Cover:

#### 1. Java 8 Features

*   **Lambda Expressions**
*   **Functional Interfaces (`Predicate`, `Function`, `Consumer`, `Supplier`)**
*   **Stream API** (Intermediate vs Terminal Operations)
*   **`Optional` class** (Avoiding `NullPointerException`)

#### 2. Design Patterns

*   **Singleton (Thread-safe ways)**
*   **Factory vs Abstract Factory**
*   **Builder Pattern**
*   **Observer Pattern**

### Practice Questions:

*   **Write a lambda to sort a list of names.**

    ```java
    import java.util.ArrayList;
    import java.util.Collections;
    import java.util.List;

    public class LambdaSortExample {
        public static void main(String[] args) {
            List<String> names = new ArrayList<>();
            names.add("Alice");
            names.add("Charlie");
            names.add("Bob");

            // Sort using a lambda expression
            Collections.sort(names, (s1, s2) -> s1.compareTo(s2));

            // Or using List.sort() directly
            // names.sort((s1, s2) -> s1.compareTo(s2));

            System.out.println(names); // Output: [Alice, Bob, Charlie]
        }
    }
    ```

*   **How to make a singleton class thread-safe?**
    *   **Eager initialization (Eager Singleton):** Create the instance at class loading time. Simple and thread-safe.
        ```java
        public class EagerSingleton {
            private static final EagerSingleton INSTANCE = new EagerSingleton();
            private EagerSingleton() {}
            public static EagerSingleton getInstance() {
                return INSTANCE;
            }
        }
        ```
    *   **Synchronized `getInstance()` method:** Synchronize the method that provides the instance. This can be slow due to lock contention.
        ```java
        public class SynchronizedSingleton {
            private static SynchronizedSingleton instance;
            private SynchronizedSingleton() {}
            public static synchronized SynchronizedSingleton getInstance() {
                if (instance == null) {
                    instance = new SynchronizedSingleton();
                }
                return instance;
            }
        }
        ```
    *   **Double-Checked Locking (DCL):** A common optimization for `synchronized` methods. Requires `volatile` for the instance variable to ensure visibility across threads.
        ```java
        public class DCLSingleton {
            private static volatile DCLSingleton instance; // volatile is crucial
            private DCLSingleton() {}
            public static DCLSingleton getInstance() {
                if (instance == null) {
                    synchronized (DCLSingleton.class) {
                        if (instance == null) {
                            instance = new DCLSingleton();
                        }
                    }
                }
                return instance;
            }
        }
        ```
    *   **Static Inner Class (Initialization-on-demand holder idiom):** The most recommended way. The inner class is loaded only when `getInstance()` is called for the first time.
        ```java
        public class InnerClassSingleton {
            private InnerClassSingleton() {}
            private static class SingletonHolder {
                private static final InnerClassSingleton INSTANCE = new InnerClassSingleton();
            }
            public static InnerClassSingleton getInstance() {
                return SingletonHolder.INSTANCE;
            }
        }
        ```
    *   **Enum Singleton:** The simplest and most robust way. Prevents reflection and deserialization issues.
        ```java
        public enum EnumSingleton {
            INSTANCE;
            public void doSomething() {
                // ...
            }
        }
        ```

*   **Difference between `map()` and `flatMap()`?**

| Feature       | `map()`                                          | `flatMap()`                                                |
| :------------ | :----------------------------------------------- | :--------------------------------------------------------- |
| **Input**     | `Stream<T>`                                      | `Stream<T>`                                                |
| **Function**  | Transforms each element into a single new element | Transforms each element into a stream of elements          |
| **Output**    | `Stream<R>` (one-to-one transformation)          | `Stream<R>` (flattens multiple streams into a single stream) |
| **Use Case**  | When you want to transform elements without changing the structure (e.g., `String` to `Integer`) | When you have a stream of collections/arrays and want to flatten them into a single stream (e.g., `List<List<String>>` to `Stream<String>`) |

---

## 📅 Day 5: Advanced Topics & Mock Interviews

### Topics to Cover:

#### 1. Memory Management

*   **Heap vs Stack Memory**
*   **Garbage Collection (Types of GC)**
*   **`OutOfMemoryError` & `StackOverflowError`**

#### 2. JVM Internals

*   **ClassLoader**
*   **JIT Compiler**

#### 3. Mock Interview & Coding Practice

*   Solve **Java coding problems** (String reversal, Fibonacci, Prime numbers)
*   Practice **multithreading problems** (Producer-Consumer, Deadlock)
*   Review **collections-based questions** (Sorting, Searching)

### Final Tips:

✔ **Revise tricky outputs** (e.g., `System.out.println(0.1 + 0.2 == 0.3);` - Output: `false` due to floating-point precision).
✔ **Prepare real-world examples** for OOP concepts.
✔ **Practice writing clean code** with proper exception handling.

---

## 🎯 Bonus: Must-Know Interview Questions

1.  **Why is `String` immutable?**
2.  **How does `HashMap` work internally?**
3.  **Difference between `ArrayList` and `LinkedList`?**
4.  **Can we override a static method?**
5.  **Explain `volatile` keyword.**
6.  **What is the diamond problem?**
7.  **How to make an object immutable?**
8.  **What is the `finally` block used for?**
9.  **Explain Java 8 Stream API.**
10. **How to prevent deadlock?**

---
