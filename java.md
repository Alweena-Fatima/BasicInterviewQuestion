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

### How HashMap Works?
The HashMap class is a component of the Java Collections Framework and resides within the java.util package. A HashMap organizes data in the form of key and a value pair where each key is mapped to it’s corresponding value. Each pair consists of one object acting as a key and another object serving as its value. When attempting to insert a duplicate key into a HashMap, the existing value mapped with that key is overwritten.   
<img width="931" height="392" alt="image" src="https://github.com/user-attachments/assets/f1113b86-03b3-41b3-98d6-fd17ecdff15d" /> <img width="594" height="444" alt="image" src="https://github.com/user-attachments/assets/492a8d48-48d4-4082-9a0a-a8ea5ca7234e" />
<img width="1137" height="228" alt="image" src="https://github.com/user-attachments/assets/e165fec8-4655-43d2-8e8d-6f7a7ee4f6ea" />  
When you put a key-value pair into a HashMap, the key’s hash code is calculated using the hashCode() method. This hash code is used to determine the index (position) where the value will be stored in an array known as the bucket.
<img width="639" height="240" alt="image" src="https://github.com/user-attachments/assets/2f58a4d8-f4eb-4fa2-bb8a-c66642a861ae" />
<img width="911" height="313" alt="image" src="https://github.com/user-attachments/assets/439a5019-e12f-4512-b48c-15acba5e618a" />
<img width="962" height="363" alt="image" src="https://github.com/user-attachments/assets/106dedc1-ea18-4543-928d-7d33fdebff73" />
<img width="856" height="574" alt="image" src="https://github.com/user-attachments/assets/86306c2a-5eea-4c38-a7ad-aafdafb70a89" />
<img width="959" height="412" alt="image" src="https://github.com/user-attachments/assets/d4b3a194-636d-45d9-ba68-0a5d2d3496cd" />
<img width="973" height="344" alt="image" src="https://github.com/user-attachments/assets/2167c2a4-2963-4057-a86c-dce87b46faa8" />
<img width="962" height="482" alt="image" src="https://github.com/user-attachments/assets/9a34bb3a-49a5-4dfd-b4c8-313b3434b6b6" />
<img width="855" height="631" alt="image" src="https://github.com/user-attachments/assets/fbf7adeb-23e1-4c00-98ed-fc8fc5f83bac" />
<img width="880" height="554" alt="image" src="https://github.com/user-attachments/assets/1f112a97-be1e-4246-8adc-eaa18af97773" />
<img width="857" height="213" alt="image" src="https://github.com/user-attachments/assets/be4bf33e-c752-453d-8715-9e0c8956705d" />









