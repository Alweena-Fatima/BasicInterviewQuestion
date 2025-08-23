# OOPs Concepts

1.) **Define OOPs?**  
Ans: OOPs, or Object-Oriented Programming, is a programming paradigm where code is organized into objects. These objects combine data and the methods that operate on that data, making programs  
more modular, reusable, and easier to maintain.

---

2.) **What are Access Modifiers?**  
Ans: Access modifiers are keywords in programming languages like Java and C++ that define the scope and visibility of classes, methods, and variables. They control which parts of a program can access a particular  
piece of code.  

- **Public** → Accessible from anywhere.  
- **Protected** → Accessible within the same package (Java) or class and derived classes.  
- **Default (package-private in Java)** → Accessible only within the same package.  
- **Private** → Accessible only within the same class.  

---

3.) **What is class?**  
Ans: these are user-defined data types.It defines the structure and behavior of objects that belong to the same type. Classes consist of fields (variables) and methods (functions).  

```java
public class classname {
    //do something
}
```

---
4. ) **What is object?**  
Ans: An object is an instance of a class, created using the blueprint provided by the class. Objects have their own state (attributes) and behavior (methods), which are defined in the class.
```java
class Car {
    void drive() {
        System.out.println("Car is driving");
    }
  }
  Car obj = new Car(); // obj is an object of class Car
  Car --> reference type(class)
  obj --> reference var
  new Car() --> object 
```
---

6. ) **What is Method ?**  
  Ans: These are functions that are defined inside a class that describe the behavior of an object. They are useful for re-usability or keeping functionality encapsulated inside one object at a time.

---

7.) **What is Constructor?**  
Ans: It is a special method in a class that is automatically called when an object of the class is created.  
  It is mainly used to **initialize the object’s state (variables)**.  
- The name of the constructor is the **same as the class name**.  
- It does **not have a return type** (not even `void`).  
```java
  class Car {
        String color;
        Car(String c) {
            color = c;
        }
        void display() {
            System.out.println("Car color: " + color);
        }
    }
    public class Test {
        public static void main(String[] args) {
            Car obj = new Car("Red"); // Constructor is called here
            obj.display();            // Output: Car color: Red
        }
    }
```

---

7. ) **Can we have Access Modifiers for Constructors?**  
  Ans: Yes, We can have it. 
    Public constructor: object can be created from anywhere.
    Private Constructor: Object cannot be created outside the class.
    Default (package-private in Java): Object can be created only within the same package.

---
    
9. ) **What is static?**  
  Ans: The keyword **`static`** in Java and C++ is used for memory management.  
       When a member (variable, method, block, or nested class) is declared as **static**, it belongs to the **class** rather than to any specific object.  
       This means all objects of the class share the same static member.  
   
   **Normal (non-static) members**  
      -Every object gets its own copy.  
      -Example: If you create 3 objects, each one has its own separate variable.  
      
```java 
      class Student {
          int id; // non-static
          Student() {
            id++; // increases for every new object
          }
      }

      If you create Student s1 = new Student(); and Student s2 = new Student();, s2= new Strudent()
      then s1.id and s2.id are different variables. value of id = 1 after creating 2 object(after each object when
      we create other the prev one gets terminated.  
  ```  

Static members belong to the class, not to objects.  
All objects share the same copy.
Memory is allocated only once (when the class is loaded).  

```java
      class Student {
              static int id; // non-static
              Student() {
                id++; // increases for every new object
              }
      }

      If you create 3 objects: then after all three object the id will be 3. here id is shared by all object

      Static Method: Can be called without creating an object.  
      syntax :      ClassName.FunctionName()---> static s=function name 

      class Dog{
        static void bark(){
           //
        }
      }
      Dog.bark();
```

---
   
11. ) **How to create object of private constructor class?**  
   Ans:If a class has a private constructor, we cannot instantiate it directly from outside the class.
       To access it, we usually provide a public static method inside the class which calls the private constructor and returns an object.
    
       **Why public static not public only?**  
       If you make a normal public method (non-static), you would need an object first to call that method.
       But the whole point is you don’t have an object yet (constructor is private!).
```java
        class MyClass {
            // Private constructor (cannot be called outside directly)
            private MyClass() {
                System.out.println("Private Constructor");
            }
            // ❌ Non-static method
            public MyClass getInstanceNonStatic() {
                return new MyClass();
            }
            // ✅ Static method
            public static MyClass getInstanceStatic() {
                return new MyClass();
            }
        }
        public class Main {
            public static void main(String[] args) {
                // MyClass obj1 = new MyClass();  // ❌ Not allowed (private constructor)
                // ❌ Non-static method can't be called without object
                // MyClass obj2 = MyClass.getInstanceNonStatic();
                // ✅ Static method can be called without creating an object
                MyClass obj3 = MyClass.getInstanceStatic();
            }
        }
```

---

13. ) **final , finally , finalize?**  
  Ans: **Final** : applied to method, variable, class --> to make them unchangeable.
```java 
        // Final variable (constant)
        final int x = 10;
        // x = 20;  ❌ Not allowed
        // Final method (cannot be overridden)
        class Parent {
            final void show() {
                System.out.println("Parent show()");
            }
        }
        class Child extends Parent {
            // void show() { } ❌ Not allowed
        }
        // Final class (cannot be inherited)
        final class Animal {}
        // class Dog extends Animal {} ❌ Not allowed
```   
Finally: used in try-catch-finally. ---> ensures a block of code always exceutes , even if exception occurs.  
        ex: Imagine you are reading data from a file. Whether reading succeeds or fails, you need to close the file to avoid resource leaks.
```java 
        try {
            int a = 10 / 0;  // This will throw exception
        } catch (Exception e) {
            System.out.println("Exception handled");
        } finally {
            System.out.println("Finally block always runs!");
        }
---
finally {
            // This block runs no matter what, ensuring the file is closed
            try {
                if (reader != null) {
                    reader.close();
                    System.out.println("File closed successfully.");
                }
            } catch (IOException e) {
                System.out.println("Error closing the file!");
            }
```

Finalize() --> method defined in object class --> alled by Garbage Collector (GC) before destroying an object 
→ used to release resources (but rarely used in modern Java, replaced by try-with-resources).

```java
        protected void finalize() throws Throwable {
            System.out.println("Finalize method called");
        }
```

---

15. ) **What is Encapsulation?**
    Ans:Encapsulation describes bundling data and methods that work on that data within one unit, like a class. We often often 
        use this concept to hide an object’s internal representation or state from the outside. This is called information hiding.
        It’s like putting the data in a capsule so that nobody can directly misuse it.  
        **How Encapsulation Works?**  
          -Make variables private → So that they cannot be accessed directly from outside.  
          -Provide public getters and setters → To safely read or update those variables.
    ```java  
        class Student {
            private String name;   // encapsulated (private)
            // setter
            public void setName(String name) {
                this.name = name;
            }
            // getter
            public String getName() {
                return name;
            }
        }
        public class Main {
            public static void main(String[] args) {
                Student s = new Student();
                //  Direct access not allowed (gives error)
                // s.name = "Alweena";  
                // Access via setter and getter
                s.setName("Alweena");
                System.out.println(s.getName()); 
            }
        }
    ```

---
    
17. ) **Inheritance ?**  
  Ans: Inheritance is an object-oriented programming concept where one class (child/subclass) 
       can inherit the properties (fields/variables) and behaviors (methods) of another class (parent/superclass).  
       If we create a Bird class with a method fly(), then any specific bird class like Owl, Parrot, or Eagle can
       inherit it and use the fly() method.
       **Parent class**--> existing class (B)  
       **Chlid class**--> new class that we are creating  (A)
    ```java
       Class A extends B{

       }
        class Bird {
            void fly() {
                System.out.println("All birds can fly");
            }
        }
        // Child class (inherits from Bird)
        class Owl extends Bird {
            void sound() {
                System.out.println("Owl hoots");
            }
        }
        public class InheritanceDemo {
            public static void main(String[] args) {
                Owl o = new Owl();
                o.fly();    // using inherited method
                o.sound();  // using child class method
            }
        }
    ```
    
Private members are inherited, but not accessible in the subclass.  
        - Types of Inheritance in Java  
              Single Inheritance  
              One child inherits from one parent.  
              Example: class B extends A  
        - Multilevel Inheritance  
              A child inherits from a parent, and another child inherits from that child.  
              Example: class C extends B, class B extends A  
        - Hierarchical Inheritance  
              Multiple child classes inherit from the same parent.  
              Example: class Dog extends Animal, class Cat extends Animal  
        - Multiple Inheritance (Not directly supported in classes)--> class c extends b,a   
              Java does not support multiple inheritance with classes (to avoid ambiguity, e.g., Diamond Problem).
              But it can be achieved using interfaces.

---

18.) **Abstraction?**  
  Ans: concept that focuses on hiding the complex implementation details and showing only the essential features of an object. It helps in 
  reducing programming complexity and effort by providing a clear separation between the abstract properties and the implementation details.  
  It can be achieve in two ways:   
  a) abstract class---> using this we can achieve 0-100% abstraction    
  b) interface (in JAVA) --> 100% abstraction   

---
                            
**19.) Abstract class?**
  Ans: we can aciheve 0-100% which means partial abstraction using abstract class
       Declared using abstract keyword 
       -- it can have abstract method(method without body) and concrete method (regular method with body)  
       --Abstract classes cannot be instantiated directly and are meant to be extended by subclasses, which means we are not allowedto create  
         object of abstract class.  
       -- Abstract class must be extended and similarly abstract method must be overidden otherwise it will throw compilation error.  
       -- if a method is abstract --> class must be abstract (Because otherwise the compiler would expect that method to have a body.)  
       -- if class is abstract --> method may/may not be abstract.(all concrete/all abstract anything)  
       
```java
        // Abstract class
        abstract class Vehicle {
            // Abstract method (no body → must be implemented by subclasses)
            abstract void start();
            // Concrete method (has a body → can be used directly)
            void stop() {
                System.out.println("Vehicle stopped.");
            }
        }
        // Subclass providing implementation for abstract method
        class Car extends Vehicle {  
            @Override
            void start() {
                System.out.println("Car started with a key.");
            }
        }  
        public class Test {
            public static void main(String[] args) {
                // Vehicle v = new Vehicle(); ❌ Not allowed (abstract class)
```

🌚Don't you wanna know why we cant create object of abstract class? simple (got this shit as interview question (selecting oops and java as fav backfires me lol))
Ans: An abstract class can contain abstract methods (methods declared but not implemented)
        
```java
        abstract class Shape {
            abstract void draw(); // no body → incomplete
        }

```
If Java let you create an object of Shape, then what would happen if you called draw()? There’s no implementation! That would break the rules of
OOPS(Every object must be able to respond to all of its methods.) but what if we have all concrete method in class? (idk the answer pls contribute)

---

15.) **polymorphism ?**  
Ans: Greek words “poly,” meaning many, and “morph,” meaning form or shape. it allows to perform simgle action in different ways( it allows us to perform multiple 
       operations by using the single name of any method (interface).)
       Java implements polymorphism in two primary forms: compile-time (or static) polymorphism and runtime (or dynamic) polymorphism.  
       
**a) --- Compile-time Polymorphism ----**  
       -  also known as static/early binding   
       -  occurs when the decision about which method to call is made at compile time.  
       - This can achieve by function overloading in java and function + operator overloading in C++  
       
**Q) ------- Function OverLoading -------?**  
         It allow us to have more than one function having same name but different Parameter list.  
         - ways to overload (function with same name-> imp we cant change the return type)   
          # changing number of parameter   
          # Data type of parameter   
          # Sequence of parameter   
```java
          public class OverloadExample {
            // 1. Different number of parameters
            public int add(int a, int b) {
                return a + b;
            }
            public int add(int a, int b, int c) {
                return a + b + c;
            }
            // 2. Different data types of parameters
            public double add(double a, double b) {
                return a + b;
            }
            // 3. Different sequence of parameters
            public double add(int a, double b) {
                return a + b;
            }
            public double add(double a, int b) {
                return a + b;
            }
            public static void main(String[] args) {
                OverloadExample obj = new OverloadExample();
                System.out.println(obj.add(2, 3));          // Calls add(int, int)
                System.out.println(obj.add(2, 3, 4));       // Calls add(int, int, int)
                System.out.println(obj.add(2.5, 3.5));      // Calls add(double, double)
                System.out.println(obj.add(2, 3.5));        // Calls add(int, double)
                System.out.println(obj.add(2.5, 3));        // Calls add(double, int)
            }
        }
```
the compiler knows exactly which add() method we are calling, based on the number/type of parameters. thats why it is compile time.
        
**Q) can we overload constructor?**    
        Ans: Yes, Sometimes there is a need of initializing an object in different ways. This can be done using constructor overloading.  
```java
            public class Box {
              double width, height, depth;
              // Default constructor
              public Box() {
                  width = height = depth = 0;
              }
              // Constructor with one parameter (cube)
              public Box(double side) {
                  width = height = depth = side;
              }
              // Constructor with three parameters
              public Box(double w, double h, double d) {
                  width = w;
                  height = h;
                  depth = d;
              }
              double volume() {
                  return width * height * depth;
              }
              public static void main(String[] args) {
                  Box b1 = new Box();
                  Box b2 = new Box(3);
                  Box b3 = new Box(2, 4, 5);
                  System.out.println("Volume b1: " + b1.volume()); // 0
                  System.out.println("Volume b2: " + b2.volume()); // 27
                  System.out.println("Volume b3: " + b3.volume()); // 40
              }
          }
```

---

**a) --- Run-time Polymorphism ----**  
        - Late Binding/Dynamic Binding  
        - Decision about which method to call is made at runtime based on the actual object's type.  
        - Achieved through method overriding.  
        - Enables dynamic method dispatch where a call to an overridden method is resolved at runtime.  
        
**Q) ---- Function Overriding -----**  
            Declaring method in subclass which is already present in parent class. overriding involves a subclass providing a specific implementation 
            for a method that is already defined in its superclass.  

**IMP------- DYNAMIC METHOD DISPATCH-------IMP**  

Dynamic method dispatch is the mechanism by which a call to an overridden method is resolved at run time, rather than compile time.
This means that the method to be called is determined at runtime based on the actual object, not on the type of reference variable. 

```java   
            Parent obj;   // this is the reference variable  
            The variable obj is a reference variable, and a reference variable stores the address of the object, not the object itself.  
            Parent obj = new Parent(); // object is created in heap Memory
```
One object is created in the heap, and the address of that object is stored in the obj variable  
Dynamic Method Dispatch: This mechanism enables a superclass reference variable to refer to a subclass object, and Java determines which 
overridden method to execute based on the actual object type.(a reference variable of the parent class can store the address of an object 
of the child class.)  

```java 
            class Parent
            {}
            class Child extends Parent
            {}
            
            Parent obj1 = new Child(); // this is valid parent class…
```
Imagine you are developing a payment system where different payment methods (Credit Card, PayPal, UPI) should have their own processing logic.  

- In DMD the object can call the overriden method and all non-overridden method of base class but it cannot call the method which are newly created and declared in a child class.
- Access modifier of overriding method cannot be more restrictive than the overriden method of parent class.

```java
class Parent {
    // A method that will be overridden
    void show() {
        System.out.println("Parent show()");
    }
    // A method that is not overridden
    void display() {
        System.out.println("Parent display()");
    }
}
class Child extends Parent {
    // Overriding the show() method
    @Override
    public void show() {   // ✅ Access modifier is same or less restrictive (public is okay here)
        System.out.println("Child show()");
    }
    // A new method only in Child
    void onlyInChild() {
        System.out.println("Child onlyInChild()");
    }
    /*
    ❌ Example of invalid override:
    protected void show() {
        System.out.println("Child show()");
    }
    // This will cause a compile-time error because
    // 'protected' is more restrictive than 'default' (package-private) in Parent
    */
}
public class Demo {
    public static void main(String[] args) {
        Parent obj = new Child(); // Reference of Parent, object of Child
        obj.show();     // ✅ Calls overridden method -> "Child show()"
        obj.display();  // ✅ Calls non-overridden method -> "Parent display()"
        // obj.onlyInChild(); 
        // ❌ Not allowed (compile-time error) because Parent reference
        // doesn't know about methods declared only in Child
    }
}
```
---

**Q) Super keyword**  
Ans: - To access attributes (fields) of the superclass if both superclass and subclass have attributes with the same name.  
     - To call methods of the superclass that is overridden in the subclass.  
     - To explicitly call superclass no-arg (default) or parameterized constructor from the subclass constructor.  

```java
class Animal {
  protected String type="animal";
}
class Dog extends Animal {
  public String type="mammal";
  public void printType() {
    System.out.println("I am a " + type);
    System.out.println("I am an " + super.type);
  }
}
class Main {
  public static void main(String[] args) {
    Dog dog1 = new Dog();
    dog1.printType();
  }
}
output :  
I am a mammal  
I am an animal
```
- Suppose Display() method is there in parent and child class overrides it now you want to call the display() of parent class?- super.method()
```java
class Parent {
    void display() {
        System.out.println("Parent display()");
    }
}
class Child extends Parent {
    @Override
    void display() {
        System.out.println("Child display()");
    }
    void show() {
        display();       // Child's display()
        super.display(); // Parent's display()
    }
}
public class Demo2 {
    public static void main(String[] args) {
        Child obj = new Child();
        obj.show();
    }
}
Child display()
Parent display()
```
```java
class Parent {
    Parent() {
        System.out.println("Parent default constructor");
    }
    Parent(String msg) {
        System.out.println("Parent parameterized constructor: " + msg);
    }
}
class Child extends Parent {
    Child() {
        super();  // calls Parent's default constructor
        System.out.println("Child default constructor");
    }
    Child(String msg) {
        super(msg); // calls Parent's parameterized constructor
        System.out.println("Child parameterized constructor: " + msg);
    }
}
public class Demo3 {
    public static void main(String[] args) {
        Child obj1 = new Child();          // default chain
        Child obj2 = new Child("Hello");   // parameterized chain
    }
}
Parent default constructor  
Child default constructor  
Parent parameterized constructor: Hello  
Child parameterized constructor: Hello
```
---
Q) **Dynamic Method Dispatch (DMD) + Constructors**  
CASE 1: When you create a Child object (say Parent p = new Child();),  
- First, the Parent’s constructor is always executed (because a child must initialize its parent first).  
- If you don’t explicitly call super(...), Java automatically inserts super(); (the no-arg constructor) as the first statement in the child constructor.  
So if the parent has only a default constructor, it gets called automatically.
```java
class Parent {
    Parent() {
        System.out.println("Parent default constructor");
    }
}
class Child extends Parent {
    Child() {
        System.out.println("Child constructor");
    }
}
public class Demo {
    public static void main(String[] args) {
        Parent obj = new Child(); // DMD applies
    }
}  
Parent default constructor  
Child constructor
```  
CASE 2: Parent has a parameterized constructor  
- If the Parent does not have a no-arg constructor, then:
- The compiler’s automatic super(); call will fail.  
You must explicitly call super(arguments...) from the child constructor to match one of the parent’s parameterized constructors.  
```java
class Parent {
    Parent(String msg) {
        System.out.println("Parent constructor: " + msg);
    }
}
class Child extends Parent {
    Child(String msg) {
        super(msg);  // ✅ Must call explicitly
        System.out.println("Child constructor: " + msg);
    }
}
public class Demo {
    public static void main(String[] args) {
        Parent obj = new Child("Hello");
    }
}
Parent constructor: Hello  
Child constructor: Hello
If you don’t write super(msg);, you’ll get a compile-time error because Java tries to insert super();, but no no-arg constructor exists.
```
---
Q) **Can we overload static method ?**  ---> yes
```java
public class Test {
    public static void foo() {
        System.out.println("Test.foo() called ");
    }
    public static void foo(int a) { 
        System.out.println("Test.foo(int) called ");
    }
    public static void main(String args[])
    { 
        Test.foo();
        Test.foo(10);
    }
}
Test.foo() called   
Test.foo(int) called
```  
We cannot overload two methods in Java if they differ only by static keyword
```java
public class Test {
    public static void foo() {
        System.out.println("Test.foo() called ");
    }
    public void foo() { // Compiler Error: cannot redefine foo()
        System.out.println("Test.foo(int) called ");
    }
    public static void main(String args[]) { 
        Test.foo();
    }
}
Compiler Error, cannot redefine foo()
```
---
Q) **Can we override static method?**  --> No,
- Static methods are class-level methods, not object-level.
- Overriding is based on runtime polymorphism (dynamic binding), but static methods are resolved at compile-time (static binding).
- If you declare a static method with the same signature in the child class, it is called method hiding, not overriding.
```java
class Parent {
    static void show() {
        System.out.println("Parent static show()");
    }
}
class Child extends Parent {
    static void show() {   // Hides Parent.show()
        System.out.println("Child static show()");
    }
}
public class Demo {
    public static void main(String[] args) {
        Parent p = new Child();
        p.show();          // Prints "Parent static show()"  (based on reference type)

        Child c = new Child();
        c.show();          // Prints "Child static show()"
    }
}
Parent p = new Child(); still calls Parent.show() because reference type decides static method resolution.
```
---
Q) **Interface?**  
- used for full abstraction
- Java interface is a reference type in Java, similar to a class, that is used to achieve abstraction and multiple inheritance.
- It defines a set of abstract methods that a class must implement. Interfaces specify what a class must do, but not how it does it.
- It can have variable and method like class but all method should be abstract.(all method are by default abstract)
- Just like abstract class we cannot create object of interface 
```java
// Define an interface
interface Animal {
    // All methods are implicitly public and abstract
    void sound();  
    void eat();
}
// Class Dog implements Animal interface
class Dog implements Animal {
    // Must provide implementation for all methods of Animal
    public void sound() {
        System.out.println("Dog barks");
    }
    public void eat() {
        System.out.println("Dog eats bones");
    }
}
public class InterfaceExample {
    public static void main(String[] args) {
        // We cannot create object of interface directly
        // Animal a = new Animal(); ❌ not allowed
        // Instead, we create objects of classes that implement the interface
        Animal dog = new Dog();  // upcasting
        dog.sound();  // Dog barks
        dog.eat();    // Dog eats bones
    }
}
```
- **Interface cannot implement another interface**
- Class implements Interface  
- Interface extends Interface
```java
interface A {
    void methodA();
}
// ❌ Not allowed
// interface B implements A {  // ERROR
//     void methodB();
// }
// ✅ Correct way: extend
interface B extends A {
    void methodB();
}
```
- **Interface extending another interface**  
- One interface can inherit methods from another.  
- The implementing class must override all inherited methods.  
```java
interface A {
    void methodA();
}
interface B extends A {
    void methodB();
}
class MyClass implements B {
    public void methodA() { System.out.println("Method A"); }
    public void methodB() { System.out.println("Method B"); }
}
```  
**Multiple Inheritance with Interfaces**  
In java you cannot have multiple inheritance but using interface you can solve diamond problem.  
Interfaces only provide method declarations (no implementation).  
So, even if two interfaces declare the same method, the child class must override it and provide its own implementation.  
This removes ambiguity, hence no diamond problem.  
```java
interface X {
    void methodX();
}
interface Y {
    void methodY();
}
// Class implementing both interfaces
class Test implements X, Y {
    public void methodX() { System.out.println("Method X"); }
    public void methodY() { System.out.println("Method Y"); }
}
```
**Diamond Problem in Interfaces**   
If two interfaces have the same default method, and a class implements both, then Java forces the class to override that method → this is how Java resolves the diamond problem safely.  
```java
interface A {
    default void show() {
        System.out.println("Show from A");
    }
}
interface B extends A {
    default void show() {
        System.out.println("Show from B");
    }
}
interface C extends A {
    default void show() {
        System.out.println("Show from C");
    }
}
class D implements B, C {
    // Compiler error if we don't resolve ambiguity
    @Override
    public void show() {
        // explicitly choose whose show() to call
        B.super.show();  // or C.super.show();
        System.out.println("Show from D");
    }
}
public class DiamondProblem {
    public static void main(String[] args) {
        D obj = new D();
        obj.show();
    }
}
Show from B  
Show from D
```







        



                
