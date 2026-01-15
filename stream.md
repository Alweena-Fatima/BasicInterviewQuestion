some better read outs : https://medium.com/javarevisited/introduction-to-java-stream-apis-25542140a279  
https://medium.com/javarevisited/introduction-to-java-stream-apis-25542140a279  
Examples: https://priyank-agarwal.medium.com/mastering-java-streams-with-complex-data-structures-45a0f4031b46
# STREAM
Java Stream API, introduced in Java 8, provides a powerful and expressive way to process sequences of elements. it easier to work with collections, such as lists or arrays, by providing a straightforward and readable approach to processing elements, instead of writing complex loops and conditionals to iterate over collections.   
Streams enable functional-style operations on collections of elements, such as filtering, mapping, and reducing. Unlike collections, streams are not data structures; they are wrappers around a data source. They allow specifying operations to be performed on the data without modifying the underlying data source.  
With Stream APIs, you can chain multiple operations together in a fluent style, making it easier to understand the sequence of transformations applied to the data in a collection.

### Before Java 8 Streams (Traditional Way)

Earlier, we processed collections using loops, which caused several problems.
- **Boilerplate Code**
You had to write long for loops even for simple tasks.  

- **Error-Prone**
Manual handling of indexes, conditions, and temporary variables could lead to bugs.  

- **No Easy Parallelism**
Making code run faster using multiple threads was complex.

- **Poor Readability & Composition**
Combining operations like filter → transform → sum was messy.

##### Example (Before Streams)

Task:
From a list of numbers, find the sum of squares of even numbers.

```java 
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5, 6);
int sum = 0;
for (int i = 0; i < nums.size(); i++) {
    if (nums.get(i) % 2 == 0) {
        sum += nums.get(i) * nums.get(i);
    }
}

System.out.println(sum);
```
👉 Problems here:  
Too many lines  
Manual logic  
Hard to read and modify

#### With the Streams in Java 8, many of these problems were addressed, offering several advantages:  
- **Declarative Syntax**: Streams provide a declarative syntax for processing collections, enabling concise and readable code.(You say what to do, not how to do it.)  
```java 
int sum = nums.stream()
              .filter(n -> n % 2 == 0)
              .map(n -> n * n)
              .reduce(0, Integer::sum);

System.out.println(sum);

```
✔ Short
✔ Readable
✔ Clear intent

- **Functional Style** : Operations like filter, map, and reduce are chained fluently.
```java 
nums.stream()
    .filter(n -> n > 2)
    .map(n -> n * 2)
    .forEach(System.out::println);

```
- **Immutable & Thread-Safe**: Streams do not modify the original collection.
```java
nums.stream()
    .filter(n -> n % 2 == 0)
    .forEach(System.out::println);
// nums remains unchanged
```
---

## How to create stream?
1️⃣ **From a Collection (Most Common Way)**: Any class that implements Collection (List, Set, etc.) can create a stream.
```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);

Stream<Integer> stream = list.stream();      // Sequential stream
Stream<Integer> pStream = list.parallelStream(); // Parallel stream
```

✅ Most used method in real projects.

2️⃣ **From an Array**
Using Arrays.stream()  
```java
int[] arr = {1, 2, 3, 4};

IntStream stream = Arrays.stream(arr);

Using Stream.of()
Stream<String> stream = Stream.of("A", "B", "C");
```

3️⃣ **Using Stream.of() (Direct Values)**
```java
Stream<Integer> stream = Stream.of(10, 20, 30);
```
---
## Stream Operations
In Java’s Stream API, operations are broadly categorized into two types: Intermediate operations and Terminal operations. Let’s break down each:

4.1. **Intermediate Operations**
- These operations transform the elements of the stream.  
- They are lazy, meaning they don’t execute until a terminal operation is called.  
- Intermediate operations return a new stream, allowing for chaining.
- Examples include map, filter, sorted, distinct, flatMap, etc.

4.2. **Terminal Operations**
- These operations produce a non-stream result.
- They execute the stream pipeline and produce a result or a side-effect.
- Once a terminal operation is invoked, the stream is consumed and cannot be reused.
- Examples include forEach, collect, reduce, count, min, max, etc. 


---

## Common Stream Operations with Examples
- **Filtering-** The filtering operations filter the given stream and returns a new stream, which contains only those elements that are required for the next operation. This is the intermediate operation.
```java 
List<Integer> numbers = Arrays.asList(1,2,3,4,5,6,7,8,9,10);

List<Integer> evenNumbers = numbers.stream()
                                   .filter(num -> num % 2 == 0) // intermediate
                                   .collect(Collectors.toList()); // terminal

System.out.println(evenNumbers);

```
- **Mapping**- Mapping operations are those operations that transform the elements of a stream and return a new stream with transformed elements.

```java 
List<Integer> squaredNumbers = numbers.stream()
                                      .map(num -> num * num)
                                      .collect(Collectors.toList());

System.out.println(squaredNumbers);

output [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

```
- **Reduction**- Reduction stream operations are those operations that reduce the stream into a single value. When we need to perform operations where a stream reduces to a single value, for example, **maximum, minimum, sum, product, etc. sum(), min(), max(), count()** etc. are some examples of reduce operations. 
```java 
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

int sum = numbers.stream()
                 .reduce(0, Integer::sum);
System.out.println(sum);
or
numbers.stream()
       .mapToInt(Employee::getSalary)
       .sum();

ans : 15
```

- **Sorting** : Sorting rearranges elements in natural or custom order.
```java 
List<Integer> numbers = Arrays.asList(5, 2, 8, 1, 9, 3);

List<Integer> sortedNumbers = numbers.stream()
                                     .sorted()
                                     .collect(Collectors.toList());

System.out.println(sortedNumbers);
```

- **counting** : Counting returns the number of elements in a stream.
```java 
List<String> names = Arrays.asList("John", "Alice", "Bob", "Emily");

long count = names.stream().count();

System.out.println(count);

```
 <img width="744" height="295" alt="image" src="https://github.com/user-attachments/assets/a7d2c469-1cfd-408c-8b3c-c0bc39e707cd" />
 <img width="856" height="523" alt="image" src="https://github.com/user-attachments/assets/91dbd77b-daeb-478e-91d1-3f7aef42732b" />

- **Slicing Operations**: Slicing means cutting the stream.      
These are intermediate operations.   
a) distinct() - remove duplicate

```java
employeeList.stream()
            .map(Employee::getCountry)
            .distinct()
            .forEach(System.out::println);

India
Canada
USA

```

b) limit(n) - takes first n elements 
```java
top 2 highest paid employee
employeeList.stream()
            .sorted((e1, e2) -> e2.getSalary() - e1.getSalary())
            .limit(2)
            .forEach(e -> System.out.println(e.getName()));

Neha
John
```
c) skip(n) - skip first n elements 
```java
employeeList.stream()
            .skip(2)
            .forEach(e -> System.out.println(e.getName()));
```

- **Matching**: these are the terminal operations, used to chcek the condition and return boolean
```java
boolean canadian =
employeeList.stream()
            .anyMatch(e -> e.getCountry().equals("Canada"));

boolean allIndian =
employeeList.stream()
            .allMatch(e -> e.getCountry().equals("India"));

boolean noneMexican =
employeeList.stream()
            .noneMatch(e -> e.getCountry().equals("Mexico"));
```
- **Finding operation** : Terminal operation, used to get the element not just true/false (findFirst(), findAny())
```java
  
Optional<Employee> emp =
employeeList.stream()
            .filter(e -> e.getCountry().equals("India"))
            .findFirst();

emp.ifPresent(e -> System.out.println(e.getName()));

```
- **Collect Operation** (collect()) : Terminal operation, converts streams into list, set, map, etc.
```java
toList()
List<String> names =
employeeList.stream()
            .map(e -> e.getName())
            .collect(Collectors.toList());

toSet()
Set<String> countries =
employeeList.stream()
            .map(e -> e.getCountry())
            .collect(Collectors.toSet());

toMap()
Map<String, Integer> map =
list.stream()
    .collect(Collectors.toMap(
        s -> s,
        s -> s.length(),
        (s1, s2) -> s1   // handle duplicates
    ));

toCollection()
LinkedList<String> names =
employeeList.stream()
            .map(e -> e.getName())
            .collect(Collectors.toCollection(LinkedList::new));

```

