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

 
