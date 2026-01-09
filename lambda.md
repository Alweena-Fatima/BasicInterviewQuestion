
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
