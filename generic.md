# Generics  
Generics allow you to write classes, interfaces, and methods that work with different data types, without having to specify the exact type in advance.

This makes your code more flexible, reusable, and type-safe.

---

### Problem without generics 
When we want to print different types of data (like Integer, String), we usually create separate methods.
```java
public class Printer {
    public void print(Integer data) {
        System.out.println("print::: " + data);
    }
    public void print(String data) {
        System.out.println("print::: " + data);
    }
}

```
#### Problems with this approach:
1️⃣ Not scalable  : What if tomorrow you want to print Double, Float, User, etc.?   You keep adding overloaded methods.  
2️⃣ Not reusable for unknown types: You cannot reuse this class for custom objects easily.  
3️⃣ Breaks DRY principle: Same logic repeated many times.

---
Generics allow us to write one reusable class that works with any data type.
```java
class Printer<T> {
    private T data;

    public Printer(T data) {
        this.data = data;
    }

    public void print() {
        System.out.println("print::: " + data);
    }
}
Printer<Integer> numberPrinter = new Printer<>(5);
Printer<String> textPrinter = new Printer<>("Hello");

```
---
### Generic Methods

Generic methods allow you to define methods with type parameters, letting them work with any type specified at runtime.

```java
public class GenericsExample {
    public static <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.println(element);
        }
    }
}
Integer[] intArray = {1, 2, 3};
String[] strArray = {"Hello", "World"};

GenericsExample.printArray(intArray);
GenericsExample.printArray(strArray);

```
---

We can create Generic classes which accepts more than 1 type. Look at the below example. It accepts an Integer and a String both.

```java 
public class MultiPrinter<T, V> {
    private final T data1;
    private final V data2;

    public MultiPrinter(T data1, V data2) {
        this.data1 = data1;
        this.data2 = data2;
    }

    public void print() {
        System.out.println("print::: " + data1 + " : " + data2);
    }
}

MultiPrinter<Integer, String> multiPrinter = new MultiPrinter<>(5, "Hello");
multiPrinter.print(); // output = print::: 5 : Hello
```

---
### Why Use Generics in Java?  
Generics provide a way to communicate to the compiler what type of data a structure should hold. This results in cleaner, safer, and more efficient code.

1. Type Safety
Generics allow you to catch type errors at compile time rather than at runtime. Without generics, you could accidentally add a String to a list intended for integers, leading to a ClassCastException later.

Without Generics: We can store any type of objects, which is risky.

```Java

List list = new ArrayList();    
list.add(10);  
list.add("10"); // No error here, but potential crash later
With Generics: The type is strictly enforced.

List<Integer> list = new ArrayList<Integer>();    
list.add(10);  
list.add("10"); // COMPILE-TIME ERROR: prevents bugs before they happen

```
2. Elimination of Casting
When you don't use generics, the compiler treats everything as a basic Object. This requires you to manually "cast" the data back to its original type when retrieving it.

Before Generics: Manual type casting is required.

```Java

List list = new ArrayList();    
list.add("hello");    
String s = (String) list.get(0); // Explicit typecasting    
After Generics: The compiler knows the type, so casting is handled automatically.

List<String> list = new ArrayList<String>();    
list.add("hello");    
String s = list.get(0); // No casting needed

```

---

### Type parameters in Generics
The type parameters naming conventions are important to learn generics thoroughly. The common type parameters are as follows:

T — Type  
E — Element  
K — Key  
N — Number  
V — Value  

---

### Bounded Type Parameters

Generics can also restrict the types that can be used, known as “bounded types.

```java 
public <T extends Number> void printDouble(T number) {
    System.out.println(number.doubleValue());
}
```

Explanation: Here, < T extends Number> means that T must be a subclass of Number, so only types like Integer, Double, Float, etc., are allowed.
```java
printDouble(5);       // Works with Integer
printDouble(5.5);     // Works with Double
// printDouble("Hello"); // Compile-time error, String is not a subclass of Number
```
---

### Wildcards (?)

Wildcards are represented by a question mark ?, and they allow unknown types in generics. There are three main types of wildcards:  

1️⃣ Unbounded Wildcard (<?>): Accepts any type.

```java
List<?> list = new ArrayList<String>();
list = new ArrayList<Integer>();
```
Explanation:
Can hold any type of list  
You cannot add elements (except null)  
Used when you only want to read data

2️⃣ Upper-Bounded Wildcard (<? extends Type>): Accepts Type or its subclasses

```java
public void printNumbers(List<? extends Number> list) {
    for (Number n : list) {
        System.out.println(n);
    }
}
```
Can accept:  
List< Integer>  
List< Double>  
List< Float>

Cannot accept:  
List< String>


You can read   
You cannot add

3️⃣ Lower-Bounded Wildcard (<? super Type>): Accepts Type or its parent classes

```java
public void addNumbers(List<? super Integer> list) {
    list.add(10);
}
```
Can accept:
List< Integer>  
List< Number>  
List< Object>

Rule:  
✔ You can add values  
❌ Reading gives Object type

---
https://medium.com/@aqilzeka99/mastering-generics-in-java-interview-questions-571232c02af9

---

### What is Type Erasure?

Type Erasure means that Java removes generic type information at runtime.

- Generics exist only at compile time,
- At runtime, Java treats them as normal objects.

Why Type Erasure Exists?

Java added Generics in Java 5, but older Java code (before generics) had to keep working.

So Java:

Uses generics for type checking at compile time  
Removes them at runtime

```java 
🔹 Simple Example
List<String> names = new ArrayList<>();
names.add("Alice");

What Java sees at runtime:
List names = new ArrayList();

➡️ String is erased
```

🔹 Another Example
```java
class Box<T> {
    T value;
}

After type erasure, it becomes:

class Box {
    Object value;
}
So T is replaced by Object.
```
🔹 Example with Bounded Types

```java
class Box<T extends Number> {
    T value;
}
After type erasure:
class Box {
    Number value;
}
```
####   Important Rule

If no bound → replaced by Object

If bound exists → replaced by that bound
