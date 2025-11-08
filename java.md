### Why we dont have pointers in java?
Java does not support explicit pointers like C or C++ to ensure safety, simplicity, and portability.  
In languages like C/C++, pointers hold direct memory addresses, allowing developers to manipulate memory manually.
However, this can lead to dangerous issues such as:  
- Memory leaks
- Dangling pointers
- Buffer overflows
- Security vulnerabilities

In Java, objects are accessed using references, which are similar to pointers but don’t expose memory addresses.
The JVM (Java Virtual Machine) manages memory — including object creation and garbage collection — ensuring safety and consistency across platforms.

##### Advantages of Not Having Pointers
Memory Safety: No direct memory manipulation prevents errors like buffer overflows and segmentation faults.  
Automatic Garbage Collection: JVM automatically frees unused memory, reducing the burden on the developer.
Platform Independence: Because memory management is handled by the JVM, Java code runs consistently across all platforms.

##### Disadvantages / Trade-offs
Performance Overhead: Garbage collection introduces slight performance overhead and unpredictable pauses.
Less Control: Developers can’t manually allocate or deallocate memory, limiting control in performance-critical systems.
Possible Memory Leaks via References: If references are held unnecessarily, garbage collection cannot reclaim the memory.

---
### Java Memory Model (JMM)
When you run a Java program, the JVM (Java Virtual Machine) divides memory into several areas.
The two main parts often discussed are:
👉 Heap Memory
👉 Stack Memory

#### 1. Heap
The Heap is the main memory pool for dynamic allocation in Java, storing all objects created during runtime.
**Key Points:**  
Used to store objects, arrays, and class instances.  
Created when the JVM starts.  
Managed automatically by the Garbage Collector (GC).  
When an object no longer has any reference, it becomes eligible for garbage collection.  
**Instance Variables and Object Allocation: When you create an object using new, it’s allocated on the heap.**  
```java 
class Car {
    public String color;
}

public class Main {
    public static void main(String[] args) {
        
        Car myCar;         // Reference type Varaiable (allocated on the stack) (pointing to null)
        myCar = new Car(); // New Car object Allocated on the heap and its reference stored on myCar on the stack.
        mycar.color = "Black"; // New String object allocated in heap and its reference is stored in instance reference variabl color of the object
    }
}

```
#### 2. Stack   
Each thread in Java has its own stack.
Stack stores:
- Method calls (stack frames)
- Local variables
- References to objects (but not the actual objects)  

**Characteristics:**  
Faster to access than heap memory.  
LIFO (Last-In-First-Out) order — when a method is called, a new block (stack frame) is pushed; when it finishes, it’s popped.  
Automatically freed when the method returns.  
```java 
public class Main {
    public void methodA() {
        int x = 5; // Stored in the stack
        Car myCar = new Car(); // Reference is in the stack; object is in the heap
    }
}
```

---

### Exception handling in java?
- The **Exception Handling in Java** is one of the powerful mechanism to handle the runtime errors so that normal flow of the application can be maintained.
```java
statement 1;  
          statement 2;  
          statement 3;  
          statement 4;  
          statement 5;//exception occurs  
          statement 6;  
          statement 7;  
          statement 8;  
          statement 9;  
          statement 10; 
```
Suppose there are 10 statements in your program and there occurs an exception at statement 5, the rest of the code will not be executed i.e. statement 6 to 10 will not be executed. If we perform exception handling, the rest of the statement will be executed. That is why we use exception handling in Java.
##### TYPE
1) Checked Exception : Checked exceptions are exceptions that are checked **at compile-time**. If a method can throw a checked exception, it must either **handle it** using `try-catch` or **declare it** using the `throws` keyword.
   they enforce the programmer to handle exceptional conditions that are **recoverable** (like file not found, database errors).

	a) IOException: Throws when input/output operation fails.
	b) FileNotFoundException: Thrown when the program tries to open a file that does not exist.
	c) SQLException: Throws when there is an error with the database.
	```java
        try {
            FileReader file = new FileReader("test.txt"); // might throw FileNotFoundException
        } catch (FileNotFoundException e) {
            System.out.println("File not found!");
        }
       // Here, `FileNotFoundException` is a **checked exception** because the compiler requires you to handle it.
        // 2. ClassNotFoundException
        try {
            Class.forName("com.example.NonExistentClass"); // Class may not exist
        } catch (ClassNotFoundException e) {
            System.out.println("Class not found: " + e.getMessage());
        }
---

2) Unchecked Exception : Unchecked exceptions are not checked at compile-time. They occur at runtime, usually due to programming errors (like logic mistakes). You don’t have to declare or handle them.
a) ArithmeticException: It is thrown when there is an illegal math operation.
b) ArrayIndexOutOfBoundsException: When you are trying to access the array index which is beyond the size of array.
c) NullPointerException: When a variable contains null value and you are performing an operation on the variable.
d) NumberFormatException – occurs when converting a string to a number if the string is invalid
e) IllegalArgumentException – occurs when a method receives an illegal argument

```java
    public class UncheckedExceptionDemo {
        public static void main(String[] args) {
    
            // 1. ArithmeticException
            int a = 10, b = 0;
            try {
                int result = a / b; // divide by zero
                System.out.println(result);
            } catch (ArithmeticException e) {
                System.out.println("Arithmetic error: " + e.getMessage());
            }
    
            // 2. NullPointerException
            String str = null;
            try {
                System.out.println(str.length()); // calling method on null
            } catch (NullPointerException e) {
                System.out.println("Null pointer error: " + e.getMessage());
            }
    
            // 3. ArrayIndexOutOfBoundsException
            int[] arr = {1, 2, 3};
            try {
                System.out.println(arr[5]); // invalid index
            } catch (ArrayIndexOutOfBoundsException e) {
                System.out.println("Array index error: " + e.getMessage());
            }
    
            // 4. NumberFormatException
            try {
                int num = Integer.parseInt("abc"); // invalid number
            } catch (NumberFormatException e) {
                System.out.println("Number format error: " + e.getMessage());
            }
    
            // 5. IllegalArgumentException
            try {
                Thread.sleep(-1000); // negative sleep time
            } catch (IllegalArgumentException e) {
                System.out.println("Illegal argument: " + e.getMessage());
            } catch (InterruptedException e) {
                e.printStackTrace(); // sleep requires handling InterruptedException
            }
        }
    }

```
##### ERROR VS EXCEPTION
- An Exception is an event that disrupts the normal flow of a program but can generally be handled by the programmer.
- An Error is a serious problem that cannot be handled by the program. It usually occurs due to hardware failure, JVM issues, or resource exhaustion.( EX: `StackOverflowError` – infinite recursion or stack overflow)
```java
public class ErrorExample {
    public static void main(String[] args) {
        // StackOverflowError example
        recursive();
    }

    public static void recursive() {
        recursive(); // infinite recursion
    }
}

```
---


