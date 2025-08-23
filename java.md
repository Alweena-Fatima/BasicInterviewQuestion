##### Exception handling in java?
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
```

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
