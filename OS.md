### What is an Operating System?
An Operating System (OS) is a system software that acts as an interface between the user and the computer hardware.  
**Functions **:
- Process Management –
Creates, schedules, and terminates processes.
(e.g., decides which process gets the CPU and for how long.)
- Memory Management –
Allocates and tracks memory for each process.
(e.g., prevents one process from using another’s memory.)
- File Management –
Manages files on disks — creation, deletion, and access control.
- Device Management –
Controls and coordinates input/output devices like keyboard, printer, etc.

--- 

### Popular operating systems
- windows
- MacOs
- Linux
- Mobile : android , ios

--- 

### What is Kernal
The kernel is the core component that manages system resources, such as CPU, memory, and hardware devices. It provides low-level services like process management, memory allocation, and device communication. Think of it as the bridge between hardware and software, ensuring that programs run smoothly and securely.  

---

### What is Shell?
The Shell is the interface between the user and the kernel.
It takes commands from the user, interprets them, and passes them to the kernel for execution.  
Shells like Bash, PowerShell, or Command Prompt provide a command-line interface (CLI) for users to interact with the OS  
In summary, the kernel handles system operations, while the shell facilitates user interaction with the OS.

---

### What is Process?
A **process** is an independent program in execution.
It has:
- Its own memory space (address space)
- Its own data, code, and system resources (like file handles, registers, etc.)
- One process cannot directly access another process’s memory

Ex: Imagine you have multiple apps open: chrome , vscode, spotify.  
Each of these are seperate process.They don’t interfere with each other’s memory directly. If Spotify crashes, Chrome still runs fine.  

---

### What is a Thread?
A thread is a smaller unit of execution inside a process.
All threads of a process:
- Share the same memory and resources of that process
- But have their own stack, registers, and instruction pointer

Think of a thread as a worker inside a process doing a specific job.  
Ex: A single process can have multiple threads. For example, your web browser process might have one thread for rendering the webpage, another for downloading a file, and a third for playing a video. All these threads live inside the same process and share its memory.
| Feature               | Process                                    | Thread                                                |
| --------------------- | ------------------------------------------ | ----------------------------------------------------- |
| **Definition**        | Independent program in execution           | Smallest unit of execution within a process           |
| **Memory**            | Each process has its own memory space      | Threads share the memory of the same process          |
| **Dependency**        | Independent of other processes             | Dependent on the parent process                       |
| **Communication**     | Requires Inter-Process Communication (IPC) | Easier, since threads share memory                    |
| **Crash Impact**      | If one process crashes, others are safe    | If one thread crashes, it may crash the whole process |
| **Creation Overhead** | Heavy (needs new memory, resources)        | Light (shares existing process memory)                |
| **Context Switching** | Slower (due to switching memory space)     | Faster (same memory space)                            |

---

### What are the different states of the process?
| **State**                      | **Description**                                                                                                                                                |
| ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 🆕 **1. New**                  | The process is **being created**. OS has not yet moved it to main memory. Example: when you open an application, it starts in this state.                      |
| ⏸️ **2. Ready**                | The process is **loaded into main memory (RAM)** and is **waiting for CPU time** to execute. Example: multiple ready processes are waiting in the ready queue. |
| 🏃 **3. Running**              | The process is **currently being executed** by the CPU. Only one process can be in the running state per CPU core.                                             |
| ⏳ **4. Waiting / Blocked**     | The process **cannot continue execution** until some event occurs (like I/O completion, user input, or resource availability).                                 |
| 🛑 **5. Terminated (or Exit)** | The process has **finished execution** or was **killed by the OS**. All its resources are released.                                                            |
---

### What is virtual memory and how does it work?
It's a memory management technique that uses a combination of physical RAM and disk space to provide the illusion of a larger, contiguous block of memory than is physically available. 
⚙️ How It Works:

- 1 Address Space:
Each process gets its own virtual address space, which is usually larger than the actual physical memory. This provides memory isolation and prevents one process from interfering with another.

- 2 Page Tables & MMU:
The Memory Management Unit (MMU) in the CPU maintains page tables that map virtual addresses to physical addresses in RAM or on disk.

- 3 Page Faults:
When a process tries to access a page that’s not in RAM, a page fault occurs. The operating system then loads that page from the disk into RAM.

- 4 Swap Space:
If RAM is full, the OS moves less frequently used pages from RAM to disk (swap space) to make room for new ones. This process is called swapping.

---

### What is a Deadlock ?
In an operating system, a deadlock occurs when two or more processes are unable to proceed because they are each waiting for the other(s) to release resources, such as locks or memory, that they need to continue.  

---
### Four Necessary Conditions for Deadlock
- **Mutual Exclusion** : At least one resource must be held in a non-sharable mode, meaning only one process can use it at a time. EX: A printer or a file can be used by only one process at a time.
- **Hold and Wait** : A process must be holding at least one resource and waiting to acquire additional resources that are currently held by other processes.
- **No Preemption** : A resource cannot be forcibly taken away from a process; it must be released voluntarily after the process is done using it.
- **Circular wait** : A circular chain of processes exists, where each process is waiting for a resource held by the next process in the chain.

### How to prevent Deadlock 
- Avoidance : Dynamic avoidance techniques involve resource allocation decisions made at runtime. These techniques use algorithms, such as the Banker's algorithm, to determine whether granting a resource request could potentially lead to a deadlock. If a request would result in a deadlock, it is denied.
- Resource Allocation Graph (RAG): Use a graph to detect and prevent circular waits by analyzing the relationship between processes and resources.
- Resource Ordering: Assign a strict order for resource acquisition and ensure all processes follow this order. This prevents the circular wait condition.
- Timeouts: If a process waits too long for a resource, it times out, releases its current resources, and retries later.

---

### What is semaphore?
A Semaphore is a synchronization tool used to control access to shared resources by multiple processes or threads.  
A semaphore is like a signal that helps threads or processes coordinate with each other so they don’t access a shared resource at the same time (which could cause conflicts).It's essentially an integer variable that can be incremented or decremented atomically and is used to manage access to critical sections of code. 
**Type**:
- Mutex : Semaphores with an initial value of 1 (binary semaphore) are often used to implement mutual exclusion. Only one process can enter a critical section at a time.
- Counting semaphores: Semaphores can also have values greater than 1, allowing multiple processes to access a resource up to a specified limit.

---

### What is context switching?
Context switching means saving the current state of a process or thread (like CPU registers, program counter, memory info) so that the CPU can load and run another one.This switch allows the operating system to efficiently manage multiple processes or threads, giving the illusion of concurrent execution on a single CPU. Context switches are essential for multitasking and ensuring that each process gets its fair share of CPU time.
**When it occurs**
⚙️ When Context Switching Occurs:
- When a process voluntarily yields the CPU.
- When a higher-priority process becomes ready.
- On a hardware or timer interrupt.
- When the scheduler preempts the current process to give CPU time to another.

---

### What is a page fault and how is it handled in an operating system?
A page fault occurs when a program tries to access a page (a fixed-size block of memory) that is not currently in the main memory (RAM).
**Steps in Page Fault Handling (Simplified Flow)**
| Step                          | Description                                                                                                                                             |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1️⃣ Trap generation**       | The CPU detects that the requested page is not in RAM and raises a **trap (page fault interrupt)**.                                                     |
| **2️⃣ OS Interrupt Handling** | The OS takes control and **pauses the process** that caused the fault.                                                                                  |
| **3️⃣ Page Table Lookup**     | OS checks the **page table entry** to see where the missing page is located (usually on the disk in the swap area).                                     |
| **4️⃣ Bring Page into RAM**   | OS selects a **free frame** in RAM. <br> If no free frame is available, a **page replacement algorithm** (like FIFO, LRU) decides which page to remove. |
| **5️⃣ Update Page Table**     | The page table entry is updated to mark the page as **present in RAM**, along with its new frame number.                                                |
| **6️⃣ Resume Execution**      | The CPU **retries the interrupted instruction**, which now finds the page in RAM and executes successfully.                                             |

---
###  What is a scheduling algorithm in an operating system and what are the different types?
In an operating system, a scheduling algorithm manages the allocation of CPU time to various processes. It decides which process gets to execute and for how long, aiming to optimize system performance.
Scheduling can be broadly classified into two types:  
**Non-Preemptive Scheduling** : Once a process starts execution, it cannot be interrupted until it finishes or voluntarily releases the CPU.
✅ Examples:
- FCFS (First-Come-First-Serve): The process that arrives first gets the CPU first. Simple but can cause the convoy effect (long waiting time for shorter processes).
- SJF (Shortest Job First) / SJN (Shortest Job Next): The process with the smallest burst time executes first. Gives optimal average waiting time but requires knowledge of burst time in advance.
- Non-Preemptive Priority Scheduling: CPU assigned to process with the highest priority until it completes.

**Preemptive Scheduling** : In this type, the CPU can be taken away from a process if a higher-priority process arrives or if the current process’s time slice expires.
✅ Examples:
- Round Robin (RR): Each process gets a fixed time quantum in cyclic order. Ensures fairness and is widely used in time-sharing systems.
- Preemptive Priority Scheduling: The CPU is allocated to the process with the highest priority, and if a new process with a higher priority arrives, it preempts the current one.
- Shortest Remaining Time First (SRTF): Preemptive version of SJF — process with the least remaining burst time is executed next.

---

### What is Thrashing?
Thrashing is a performance degradation situation in an operating system that occurs when the system spends most of its time swapping pages between main memory (RAM) and disk, instead of executing actual processes.  
In other words, Thrashing occurs when a system spends more time processing page faults than executing transactions. 
**Key Characterstics of Thrashing**:
- High Disk Activity: The system constantly reads and writes pages to and from disk.
- Low CPU Utilization: CPU is underutilized because it waits for pages to be loaded from disk.
- Frequent Page Faults: Pages required by processes are not in memory, causing frequent page faults.

---
### What is cache memory in an operating system?
Cache memory in the context of an operating system is a small, high-speed volatile storage that sits between the main memory (RAM) and the central processing unit (CPU).

---
### Memory allocation?
Memory allocation is the process by which the operating system assigns portions of main memory (RAM) to various processes so that they can execute efficiently without interfering with each other.
It ensures that:
- Each process gets enough memory to run.
- Memory is used efficiently.
- Processes do not access each other’s memory space.

**Type**:  
**1.Fixed Partitioning**
- The main memory is divided into fixed-size partitions.
- Each partition holds exactly one process.
- Drawback: Leads to internal fragmentation (unused space inside partitions).
- Example: If a 100 MB partition runs a 70 MB process → 30 MB wasted.

**2.Dynamic Partitioning**
- Memory is divided dynamically based on the process size.
- Reduces internal fragmentation but can cause external fragmentation (small free holes scattered across memory).
- Solution: Use compaction (combine free spaces).

---
### 3. Paging 
It allows the 
- logical memory (virtual memory) of a process to be divided into fixed-size blocks called pages, and 
- the physical memory (RAM) to be divided into blocks of the same size called frames.

The operating system keeps a page table to map each page of a process to a specific frame in physical memory.
How Paging Works (Step-by-Step):
- The process is divided into pages of equal size (say, 4 KB each).
- The main memory (RAM) is divided into frames of the same size.
- When the process runs, some pages of it are loaded into available frames.
- The page table keeps track of which page is in which frame.
- When the CPU needs to access an address, it uses the page number and offset to find the correct frame in RAM.

Eliminates external fragmentation but may cause internal fragmentation (unused space within a frame) and Page table overhead: Each process needs its own page table.

---

### 4 Segmentation
Segmentation is a memory management technique in which the logical memory of a process is divided into variable-sized segments, based on the logical divisions of a program, such as functions, data, stack, or objects.  
Unlike paging, which divides memory into fixed-size blocks, segmentation divides memory according to the program’s logical structure.
| Term                 | Meaning                                                                         |
| -------------------- | ------------------------------------------------------------------------------- |
| **Segment**          | A variable-sized block representing a logical unit (like code, data, or stack). |
| **Segment Table**    | Stores the base address (starting point) and length (size) of each segment.     |
| **Logical Address**  | Consists of: **Segment Number + Offset**.                                       |
| **Physical Address** | Calculated by: **Base Address + Offset** (checked against segment length).      |

🧠 How Segmentation Works:
- Each program is divided into segments.
- Each segment can have different lengths based on actual need.
- The segment table keeps track of each segment’s base address (start location in physical memory) and limit (length).
- When a process needs a particular memory address, the OS translates the logical address (segment number, offset) into a physical address using the segment table.

Provides a logical view of memory and no internal fragmentation (since segments are variable-sized) but Can lead to external fragmentation, as segments are variable-sized.
