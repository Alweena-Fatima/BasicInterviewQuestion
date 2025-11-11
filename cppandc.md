### Dynamic Memory Allocation in C
In C programming, dynamic memory allocation refers to the process of allocating memory during runtime. This means that memory is allocated to a program only when it is executed, rather than at compile time. This allows for more flexibility in managing memory and can help prevent issues such as running out of memory or wasting memory on unused variables.(using functions from <stdlib.h>.)  
#### Functions for Dynamic Memory Allocation   
**1. malloc() → Memory Allocation**  
The `malloc()` function stands for “memory allocation” and is used to allocate a block of memory on the heap. The function takes a single argument, which is the size (in bytes) of the memory block to be allocated. 
- The function returns a pointer to the first byte of the allocated memory block.
- Contents are not initialized (contain garbage values).
- Returns NULL if allocation fails.

```c
int *ptr = (int*)malloc(sizeof(int));
*ptr = 5;
printf("%d", *ptr);
free(ptr);

```
1. The `malloc()` function allocates a block of memory on the heap.
2. The `ptr` variable on the stack stores a pointer to the first byte of this memory block.
3. The value 5 is assigned to the memory location pointed to by `ptr`.
4. The `free()` function deallocates the memory block on the heap.  

**2 . calloc() → Allocates memory for multiple elements**  
The `calloc()` function is similar to `malloc()`, but with two key differences. First, `calloc()` takes two arguments: 
- the number of elements to be allocated and the size (in bytes) of each element. 
- Second, `calloc()` initializes the allocated memory block to zero.

```c
int *ptr = (int*)calloc(5, sizeof(int));
for(int i=0; i<5; i++)
    printf("%d ", ptr[i]); // prints 0 0 0 0 0
free(ptr);

```
1. The `calloc()` function allocates a block of memory on the heap and initializes it to zero.
2. The `ptr` variable on the stack stores a pointer to the first byte of this memory block.
3. The values of the array elements are printed.
4. The `free()` function deallocates the memory block on the heap.  

**3 . free() → deallocates the memory**
The `free()` function is used to deallocate a block of memory that was previously allocated using `malloc()`, `calloc()`, or `realloc()`.  
The function takes a single argument, which is a pointer to the first byte of the memory block to be deallocated.  
It is important to note that once a block of memory has been deallocated using `free()`, it should not be accessed again. Attempting to access deallocated memory can result in undefined behavior.
```c
int *ptr = (int*)malloc(sizeof(int));
*ptr = 10;
free(ptr);
// ptr should not be used now
```
**4. realloc() : Reallocation / Resize**  
The `realloc()` function is used to change the size of a previously allocated memory block. The function takes two arguments:
- a pointer to the first byte of the memory block to be reallocated and 
- the new size (in bytes) of the memory block.  

If the new size is larger than the original size, additional memory will be allocated at the end of the original block. If the new size is smaller than the original size, the excess memory at the end of the original block will be deallocated.  
```c
int *ptr = (int*)malloc(2 * sizeof(int));
ptr[0] = 1; ptr[1] = 2;
for(int i=0; i<2; i++)
    printf("%d ", ptr[i]); // 1 2
    
ptr = (int*)realloc(ptr, 4 * sizeof(int));
ptr[2] = 3; ptr[3] = 4;
for(int i=0; i<4; i++)
    printf("%d ", ptr[i]); // 1 2 3 4
free(ptr);

```
1. The `malloc()` function allocates a block of memory on the heap.
2. The `ptr` variable on the stack stores a pointer to the first byte of this memory block.
3. Values are assigned to the first two elements of the array.
4. The `realloc()` function increases the size of the memory block on the heap.
5. Values are assigned to the additional elements of the array.
6. All elements of the array are printed.
7. The `free()` function deallocates the memory block on the heap.


### Dynamic Memeory Allocation in c++
In C++, stack memory is automatically allocated for variables at compile time and has a fixed size. For greater control and flexibility, dynamic memory allocation on the heap is used, **C++ provides new and delete for dynamic memory management (manual control).**
This is useful when the size of required memory isn’t known at compile time, such as for variable-sized arrays or dynamic data structures like linked lists and trees.  

#### 1. new Operator: 
Allocates memory from the heap (Free Store) at runtime and returns the address of the allocated block.  
```cpp
pointer = new data_type;          // single variable
pointer = new data_type[size];    // array

int *ptr = new int(6);
cout << *ptr;   // Output: 6
cout << ptr;    // Prints address

```
⚠️ If Memory Not Available:  
new throws std::bad_alloc exception if the allocation fails.  
To avoid exceptions, use nothrow:  
```cpp
int *p = new (nothrow) int;
if (!p) {
    cout << "Memory allocation failed\n";
}
```
##### 2. delete Operator
Used to free memory that was allocated using new.   
```cpp 
delete ptr;       // delete single variable
delete[] ptr;     // delete an array
```
#### Errors Associated with Dynamic Memory
**1. Memory Leaks** : Memory leak is a situation where the memory allocated for a particular task remains allocated even after it is no longer needed. Moreover, if the address to the memory is lost, then it will remain allocated till the program runs.  
```cpp
int* ptr = new int(5);
ptr = new int(10);   // Memory for 5 is lost — leak occurs
```
**2. Dangling Pointer**: Dangling pointers are created when the memory pointed by the pointer is accessed after it is deallocated, leading to undefined behaviour (crashes, garbage data, etc.).  

Solution: Initialize pointers with nullptr and assign nullptr again when deallocated.
```cpp
int* ptr = new int(10);
delete ptr;
cout << *ptr;   // ❌ Dangling pointer (memory freed)

delete ptr;
ptr = nullptr;
```
**3. Double Deletion**: When delete is called on the same memory twice, leading to crash or corrupted program.  
Solution: assign nullptr to the memory pointer when deallocated.  
```cpp
int* ptr = new int(20);
delete ptr;
delete ptr;  // ❌ double delete

delete ptr;
ptr = nullptr;
```
---

### Friend Function in c++
A friend function is a non-member function that is given special access to a class’s private and protected members by declaring it a friend inside the class.    
A friend function is declared inside the class but defined outside, making it different from regular member functions. It allows external functions to interact with private data without making them part of the class itself. 

---

### Why do we need friend function when we already have member function?
A member function belongs to only one class, so it cannot directly access private data of another class.  
But a friend function can be made a friend of multiple classes!
```cpp
class A {
    int dataA;
public:
    A(int val) : dataA(val) {}
    friend void showSum(A, B);  // declared later
};

class B {
    int dataB;
public:
    B(int val) : dataB(val) {}
    friend void showSum(A, B);  // same friend function
};

void showSum(A obj1, B obj2) {
    cout << obj1.dataA + obj2.dataB;  // can access both
}

```

####  Global Function as a Friend Function in C++

```cpp
#include <iostream>
using namespace std;
class A {
private:
    int data;
public:
    A(int val) : data(val) {}
    // Declaring a global function as a friend
    friend void displayData(A obj);
};
// Global function definition
void displayData(A obj) {
    cout << "Private data: " << obj.data << endl;  // Accessing private member
}
int main() {
    A obj(10);
    displayData(obj);  // Calling the friend function
    return 0;
}

```

#### Member Function of Another Class as a Friend Function in C++

```cpp
#include <iostream>
using namespace std;
class B;  // Forward declaration
class A {
private:
    int dataA;
public:
    A(int val) : dataA(val) {}
    // Declaring a member function of class B as a friend
    friend void B::showData(A obj);
};

class B {
public:
    void showData(A obj) {  
        cout << "Private data of A: " << obj.dataA << endl;  // Accessing private member of A
    }
};

int main() {
    A objA(20);
    B objB;
    objB.showData(objA);  // Calling the friend member function
    return 0;
}
```
---
### Friend Class?
A friend class is a class that has access to the private members and protected memberof another class. Instead of making individual functions friends, an entire class is given special access.  
If class B is a friend of class A, then all member functions of B can access private and protected members of A.

```cpp
class A {
private:
    int secret = 42;

    // Declare B as a friend
    friend class B;
};

class B {
public:
    void showSecret(A obj) {
        cout << "Secret: " << obj.secret;  // ✅ allowed
    }
};

```
🚫 Important Note: Friendship is not mutual and not inherited.  
```cpp
class A {
    friend class B;
private:
    int dataA = 10;
};
class B {
public:
    void show(A obj) { cout << obj.dataA; }  // ✅ works
};
class C : public B {
public:
    void test(A obj) { 
        // cout << obj.dataA; ❌ ERROR — not inherited
    }
};

```
Even though B is a friend of A, its derived class C is not automatically a friend.  
Use When : When multiple functions need access to private members instead of just one.  

---
### Virtual function?
A virtual function is a member function in a base class that you can override in a derived class.  
When a function is declared as virtual, C++ uses runtime (dynamic) polymorphism to decide which version of the function to call — the one in the base class or the one in the derived class — based on the actual type of the object.

```cpp
#include <iostream>
using namespace std;
class Base {
public:
    virtual void show() {  // declared as virtual
        cout << "Base class function\n";
    }
};
class Derived : public Base {
public:
    void show() override {  // override keyword is optional but recommended
        cout << "Derived class function\n";
    }
};

int main() {
    Base* ptr;
    Derived obj;
    ptr = &obj;
    ptr->show();   // ✅ Calls Derived’s show(), not Base’s (runtime polymorphism)
}

Derived class function
If show() wasn’t declared as virtual, the output would be:

Base class function
```
---

### What is a Vtable?
A vtable (virtual table) is an internal data structure generated by the C++ compiler to support runtime polymorphism.  
It acts as a lookup table of function pointers that stores the addresses of virtual functions for a particular class.  
Each class that has virtual functions maintains its own vtable, and every object of such a class contains a hidden pointer called the vptr (virtual pointer), which points to the class’s vtable.
🔹 How the Vtable Works

- Creation of Vtable: When a class with virtual functions is compiled, the compiler creates a vtable for it. The vtable holds pointers to all virtual functions defined in the class.

- Initialization of Vptr: Each object of the class stores a hidden vptr. When the object is created, the vptr is automatically set to point to that class’s vtable.

- Virtual Function Call : When a virtual function is called (via a base class pointer/reference), the compiler uses the vptr to find the correct function address in the vtable, and calls it. This ensures that the function corresponding to the actual type of the object (not the pointer type) is executed.
 
```cpp
#include <iostream>
using namespace std;

class Base {
public:
    virtual void show() { cout << "Base show()\n"; }
};

class Derived : public Base {
public:
    void show() override { cout << "Derived show()\n"; }
};

int main() {
    Base* ptr = new Derived();
    ptr->show();   // Output: Derived show()
}

```
Base class me ek virtual function show() hai.
→ Compiler Base ke liye ek vtable banata hai jisme Base::show() ka address hota hai.

Derived class ne show() ko override kiya.
→ Compiler Derived ke liye ek nayi vtable banata hai jisme Derived::show() ka address hota hai.

Jab Derived ka object banta hai,
uske andar ek vptr hota hai jo Derived vtable ko point karta hai.

Jab ptr->show() call hota hai,
toh program vptr ke through Derived vtable me jata hai
aur Derived::show() call karta hai.

---
### What is a Pure Virtual Function?
A pure virtual function is a virtual function with no definition (no body) in the base class — it is meant to be overridden by derived classes.

```cpp
virtual void functionName() = 0;
```

```cpp
#include <iostream>
using namespace std;
class Shape {
public:
    // Pure virtual function
    virtual void draw() = 0;  
};
class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing Circle" << endl;
    }
};

class Square : public Shape {
public:
    void draw() override {
        cout << "Drawing Square" << endl;
    }
};
int main() {
    Shape* s1 = new Circle();
    Shape* s2 = new Square();

    s1->draw();   // Output: Drawing Circle
    s2->draw();   // Output: Drawing Square
}


```

---
### What is an Abstract Class in C++?
An abstract class is a class that cannot be instantiated (you can’t create objects of it).
It is designed to be a base class, meaning it provides a common interface for all derived classes.  
**A class becomes abstract when it has at least one pure virtual function.**
```cpp
class Shape {
public:
    virtual void draw() = 0; // pure virtual function
};
```
Shape is abstract class   
**Why Use Abstract Classes?**  
Abstract classes are used when:  
You want to force derived classes to implement certain functions.  
You want to create a common interface for multiple classes.  

---

### What is Operator Overloading?
Operator Overloading means giving new meaning to an existing operator for user-defined data types (like classes or structs).  
In simple words:  
C++ allows you to redefine how operators (+, -, *, ==, etc.) behave when used with objects.
<img width="993" height="574" alt="image" src="https://github.com/user-attachments/assets/005754f1-9099-4167-8181-127191e4ca3c" />
<img width="994" height="440" alt="image" src="https://github.com/user-attachments/assets/d11cc5dd-a51d-403b-9067-602d943c4675" />
```cpp
#include <iostream>
using namespace std;

class Complex {
    int real, imag;

public:
    Complex(int r = 0, int i = 0) {
        real = r;
        imag = i;
    }

    // Operator overloading function
    Complex operator+(Complex obj) {
        Complex result;
        result.real = real + obj.real;
        result.imag = imag + obj.imag;
        return result;
    }

    void display() {
        cout << real << " + " << imag << "i" << endl;
    }
};

int main() {
    Complex c1(2, 3);
    Complex c2(4, 5);

    Complex c3 = c1 + c2; // uses overloaded +
    c3.display();          // Output: 6 + 8i
}



```

---

<img width="914" height="351" alt="image" src="https://github.com/user-attachments/assets/461923a4-9618-431d-ba27-a2bed8946f4e" />
<img width="1025" height="359" alt="image" src="https://github.com/user-attachments/assets/dc8d7dac-bb55-4f2e-8ebe-f7db993814d7" />
<img width="932" height="660" alt="image" src="https://github.com/user-attachments/assets/8bc6037c-27d6-44b2-a21d-d05512f4fa02" />





