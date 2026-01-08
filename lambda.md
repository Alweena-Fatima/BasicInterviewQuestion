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

---


# LAMBDA

Lambda functions, introduced in Java 8, are anonymous functions that can be treated as values and passed around as arguments to methods.  
In other words, a lambda function is a concise way to represent a block of code that can be executed later. It is a way to define functions inline, without having to create a formal method with a name, return type, or access modifiers.

- No name 
- No modifier 
- No return type 

### SYNTAX

```java 
(parameter list) -> { body }

```

#### Parameter List: 
It specifies the parameters that the lambda function takes. If there are no parameters, an empty set of parentheses is used.  
#### Arrow Operator (->): 
The arrow operator separates the parameter list from the body of the lambda function.
#### Body: 
It represents the implementation of the lambda function. If the body contains a single statement, curly braces `{}` can be omitted. If the body contains multiple statements, curly braces are required.

---

### Benefits of Using Lambda Functions

- **Conciseness** : They allow developers to express their intentions more concisely, focusing on the actual logic of the function rather than its definition.  

**without Lambda**
```java 
class Main {
    public static void main(String[] args) {
        List<Integer> list = Arrays.asList(5, 2, 8, 1);

        Collections.sort(list, new Comparator<Integer>() {
            public int compare(Integer a, Integer b) {
                return a - b;
            }
        });

        System.out.println(list);
    }
}
```

**with Lambda**
```java 
class Main {
    public static void main(String[] args) {
        List<Integer> list = Arrays.asList(5, 2, 8, 1);

        Collections.sort(list, (a, b) -> a - b);

        System.out.println(list);
    }
}
```

- **Flexibility** : Lambda functions can be used in various scenarios, such as filtering collections, mapping elements, and performing computations on data. 

```java 
// Filtering using lambda function
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
List<String> filteredNames = names.stream()
                                  .filter(name -> name.startsWith("A"))
                                  .collect(Collectors.toList());

```

- **Readability** : Lambda functions improve code readability by providing a more natural way to represent simple functions.

---

1️⃣ Use Lambda Expressions for Functional Programming

Functional programming focuses on what to do, not how to do it.

Example
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

numbers.stream()
       .filter(n -> n % 2 == 0)
       .map(n -> n * n)
       .forEach(System.out::println);

```
✔ filter() → selects even numbers  
✔ map() → squares numbers  
✔ forEach() → prints result  

2️⃣ Use Lambda Expressions to Create Anonymous Classes

Lambdas replace anonymous inner classes.

Example (Runnable)
```java
Runnable r = () -> System.out.println("Thread running");
new Thread(r).start();
```

✔ Shorter than anonymous class  
✔ Implements run() method directly

3️⃣ Use Lambda Expressions for Event Listeners

Used in GUI programming.

Example (Button Click)
```java 
button.addActionListener(e -> System.out.println("Button clicked"));
```

✔ Executes code when event occurs

4️⃣ Use Lambda Expressions to Iterate Collections

No need for loops.

Example (List)
```java
List<String> fruits = Arrays.asList("apple", "banana");
fruits.forEach(f -> System.out.println(f));

Example (Map)
map.forEach((k, v) -> System.out.println(k + " : " + v));
```

5️⃣ Use Lambda Expressions to Filter Collections

Select required elements.

Example
```java
List<Integer> even =
numbers.stream()
       .filter(n -> n % 2 == 0)
       .collect(Collectors.toList());

```
✔ Keeps only even numbers

6️⃣ Use Lambda Expressions to Sort Collections

Defines sorting logic easily.

Example (Descending order)
```java
words.stream()
     .sorted((a, b) -> b.compareTo(a))
     .collect(Collectors.toList());
```
7️⃣ Use Lambda Expressions to Map Collections

Transforms elements.

Example
```
List<String> upper =
words.stream()
     .map(s -> s.toUpperCase())
     .collect(Collectors.toList());

```
✔ Converts strings to uppercase

8️⃣ Use Lambda Expressions to Reduce Collections

Produces single result.

Example (Sum)
```
int sum = numbers.stream()
                 .reduce(0, (a, b) -> a + b);

```
✔ Adds all elements

9️⃣ Use Lambda Expressions to Group Collections

Groups elements by condition.

Example
```java
Map<Integer, List<String>> group =
words.stream()
     .collect(Collectors.groupingBy(String::length));
```

✔ Groups words by length

🔟 Use Lambda Expressions to Handle Null Values

Prevents NullPointerException.

Example
```java
list.stream()
    .filter(s -> s != null)
    .forEach(System.out::println);
```
1️⃣1️⃣ Use Lambda Expressions for Parallel Processing

Faster execution.

Example
```java
int sum = numbers.parallelStream()
                 .mapToInt(n -> n)
                 .sum();
```
1️⃣2️⃣ Use Lambda Expressions with Method References

Shorter syntax.

Example
```java
numbers.forEach(System.out::println);


✔ Replaces n -> System.out.println(n)
```
1️⃣3️⃣ Use Lambda Expressions with Default Methods

Default methods work with lambdas.

Example
```java
Calculator c = (a, b) -> a + b;
System.out.println(c.subtract(5, 3));
```

---
