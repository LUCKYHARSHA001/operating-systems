# Operating Systems
---

**Aurthor**: Harsha Vardhan

---

## 🚀overview:
  In this Documentation we will mainly focus on

1. Fundementals
  - Evolution of OS
  - System Components
  - OS Architectures
  - Boot Process

2. Process Management
  - Process Concept
  - Threads
  - CPU Scheduling
  - Inter-Process Communication

3. Process Synchronization
  - Critical Section Problem
  - Synchronization Tools
  - Classic Problems
  - Deadlocks

4. Memory Management
  - Basics
  - Contiguous Allocation
  - Non-Contiguous Allocation
  - Virtual Memory

5. Storage & File Systems
  - File Concept
  - Directory Structure
  - File System Implementation
  - Mass-Storage Structure
  - Disk Scheduling

6. I/O Systems
  - Hardware
  - Communication
  - Kernel I/O Subsystem
  - Device Drivers

---

## 1. Fundamentals

### 1.1 Evolution of OS:

| Era | Focus | Key Technology |
| :--- | :--- | :--- |
| 1940s | Bare Machine | Switches & Wires |
| 1950s | Job Automation | Batch Processing |
| 1960s | CPU Utilization | Multiprogramming |
| 1970s | User Interaction | Time-Sharing (UNIX) |
| 1980s | Accessibility | GUI (Windows/Mac) |
| Modern | Connectivity | Mobile & Cloud |

### 1.2 System Components:
  Basically in systems components there comes the shell , the system libraries and the kernal
  - Shell (Outer Layer):  
  it is the **user Interface** of the operating system . It is the actually part us the human see and interact with  
  Its job is to take our input, understand it and pass into deeper system like **CLI and GUI**.
  
  - System Libraries (The Middleman):  
  The programs **directly cant talk to the kernel** because the kernel language is very complex so instead we use system Libraries
  - Kernel (The Heart):  
  It is the core of the OS and it has complete control over everything in the system, it starts when the computer boot and ends when it shuts down untill then it stays in the memory  
  It has the control over resource management and privilage mode  
  Resource Maangaement:It decides which proccess gets the cpu and RAM it can use and handles data storage  
  Priviliged Mode: kernel runs in **Kernel Mode** means it can do any thing in the system and this is a protected area if the normal app(user mode) crashes, the system still stays up and if the kernel crashes the blue screen appears

### 1.3 OS Architectures:
  - Monolithic Kernels:  
  in this the entire operating system including device drivers, file systems, and network stacks—runs in a single address space within the kernel.  
  mechanism: Components communicate through direct function calls.  
  adv: High performance  
  dis: f one driver crashes, the entire system will go stop
  - Microkernels:  
  in this it minimizes the kernel to the absolute essentials: address space management, thread scheduling, and Inter-Process Communication and remaining the drivers and file systems in user mode  
  mechanism: When a user application needs a file, the microkernel acts as a postman  
  adv: High reliability and security.
  dis: Slower than monolithic kernels
  - Hybrid Kernels:
  in this it tries to combine the speed of a monolithic kernel with the modularity of a microkernel.  
  mechanism: It keeps a microkernel-like structure but allows **servers** to run inside the kernel's address space.
  adv: Balanced performance and stability.

|Feature| Monolithic | Microkernel | Hybrid|
| :--- | :--- | :--- | :---|
| Kernel Size |	Large |	Very Small |	Medium |
| Execution |	All in Kernel Mode |	Mostly User Mode |	Mixed|
| Stability |	Lower (One fail = Crash) |	High (Isolate fails)	| Medium/High |
| Performance	| Maximum	| Lower (IPC overhead)	| Balanced |

### 1.4 Boot Process :  


---

## 2. Process Management

### 2.1 Process:  
  **Mainly the process is known as the program in execution** .  
  The layout of process in memory
  ![Alt text](./assets/layout_of_proceess.png)  
  1. Text: the executable code
  2. Data: the global variables
  3. Heap: memory that dynamically allocated during program run time
  4. Stack: temporary data storage when invoking functions(eg: local variables etc..)  
  We can observe that the text and data sections are fixed while heap and stack sections are not because they can grow dynamically during program execution.  
  A program becomes an process when an executable file is loaded into memory.  
  Even if the two processes may associated with the same program they are considered as two seperate execution sequence.

  - Process State:  
  As a process executes, its state changes. the state of process is defined in part by the current activity of that process.
  In this there are states  
  1. New: the process is being created
  2. Running: Instructions are being executed  
  3. Waiting: the process is waiting for event(ex: I/O completion of signal)  
  4. Ready: the process is waiting to assigned to a processor
  5. Terminated: The process has finished execution  
    
  ![Alt text](./assets/process_state.png)  
  - Process Control Block:  
  In OS each process is represented by a process control block(PCB) which is also known as task control Block . it has many specific process blocks like  
  1. Process state: the state may be new,ready,running,waiting.....  
  2. Program counter:This indicates the address of the next instruction to be executed for this process.  
  3. CPU Registers: This is used when an interrupt occours  it allows the process to be continued correctly afterward when it rescheduled to run.  
  4. CPU Scheduling Information: This includes the process priority, pointers to scheduling queues etc  
  5. Memory management information: it stores the information like page tables, segment tables etc based on the memory system  
  6. Acounting Information: this has the amount of **CPU and realtime used** etc.  
  7. I/O status information: this has the list of input output devices allocated to the process, a list of open files etc  

  ![Alt Text](./assets/pcb.png)  

  ### 2.2 Threads:  
  In operating System thread is the smallest executable unit in the process and it is the actual entinty that executes the code  
  - Process vs Thread:  
  process:It is the heavy execution unit that has its own address space  
  Thread: It is called as light-weight process exists inside the process and shares its data or resources  
      - Shared Resources: Code section, data section, and OS resources
      - Unique Resources: Each thread has its own Program Counter (PC), Stack, and Register Set.
  
  - Types of Threads:  
  User-Level Threads:These are the threads managed by the user-sspace library unlike the operating system kernel, and the kernel is unaware of these existance and sees it as a single thread.  
  Kernel-Level Thread:These are the threads directly managed by the kernel operating system.  

  - Multithreading Models: In os the architects use different mapping models for the gap between user level threads and kernel level threads  
    |Model|Description|
    |:---|:---|
    |Many-to-One|Many user threads map to one kernel thread. If one blocks, all block|
    |One-to-One|Each user thread maps to a kernel thread. Provides best concurrency|
    |Many-to-Many|Many user threads are multiplexed to a smaller or equal number of kernel threads.|

  - Benefits of Multithreading:  
  Responsiveness: application can be interactive even it already doing another work  
  Resource Sharing: Threads share memory by default, making communication easier than Inter-Process Communication (IPC)  
  Economy:Creating and context-switching threads is much "cheaper" than processes.

  - Critical Issues in Threading:  
  Race Conditions: when the two or more threads try to access the shared data at the same time the outcome is based on the order of execution  
  Deadlocks: As the name says its a case where **Thread A waits for resource hold by Thread B** and **Thread B waits for the resource hold by Thread A** leading to the problem where the threading stucks with out moving  
  Context Switching Overhead: While lighter than processes, switching between too many threads still consumes CPU cycles

  ### 2.3 CPU scheduling:
  Normally in a System with a single CPU core only one process can run at a time and other processes must wait until the CPU's core is free and thenn it moves to next process in thee mean time while in the process is executing it will wait for some time for the completion of I/O request etc which makes the **CPU sits idle** and all the waiting time is wasted.
  So we came up with a solution called **MultiProgramming**  
  Multiprogramming: In this we use this time productively by in that waiting time instead of making the system wait idlely we will let another proccess to do its thing in that waiting time and this way continues as it keeps the CPU busy to the fullest  
  So in CPU scheduling the CPU will select a process from the processes in the memory that are ready to executed and allocates the cpu to that process and we should remeber that **ready queue may follow First-in First-out(FIFO)queue or priority queue or tree etc..  
  So the CPU-scheduling decisions will takes place under 4 conditions  
  1. when a process switches from running state to waiting state
  2. when a process Terminates
  3. when a process switches from running state to ready state
  4. when a process switches from waiting state to ready state

  So in this the first two conditions comes under **Preemptive Scheduling** and third and fourth conditions comes under **non-Preemptive Scheduling**  
  In non-preemption Scheduling once the CPU is been allocated to a process the process keeps the CPU until it releases it either by termination or by switching to waiting state  
  In preemptive it can result in race conditions when the data is shared among several processes

  - Dispatcher:
  It is a component in CPU-scheduling used to give control of the CPU's core to the process selected by CPU scheduler and it also do things like
    - switching context from one process to another
    - Switching to user mode
    - Jumping from proper location in the user program to resume that program
  The time it takes for the dispatcher to stop one process and start another running is known as dispatch latency  
  ### 2.4 Inter Process Communication:  
  while processes are executing in a os it will be either **independent or cooperating process**  
  Independent Process: it is known as independent if it does **not share data** with other processes while executing.
  Co-operating Process: in this it can share data to other processs which lead to effect other process while executing.  
  This Co-operating process require a mechanism that helps to communicate and exchange data between them and this is known as IPC(Inter Process Communication).  
    
  In IPC there are 2 main models:
  1. Shared memory: it is a region of memory that is shared by co-operating processes is established    
  2. message passing:in this the communication takes place by exchanging messaging between the co-operating systems.  
  **IPC in Shared memory:**  
  As we known the os normally tries to prevent one process to access other access so in shared memory we will get a region means address space of the process creating and then the process which wish to communicaate will come and attach to the address space leading communication or sharing data between processes  
  And also there own processes are responsible to makesure that no two process write at the same location simultaneously  
  **IPC in Message-passing:**  
  This provides a mechanism to communicate and sychronize between them.  
  Commonly a message will be either have a fixed size or variable size  
  **If fixed size:** then the system level implementation is straight forward but the programming this task is difficult.  
  **If Variable Size:** then the system level implementation is difficult and programming this task is easy.  
  But for 2 processes like P and Q to communicate between them then there must be a communication link that is established between them.for this we connect them we have several methods for logically implementing a link  
    1. Direct or indirect Communication  
    2. Synchronous or Asynchronous Communication  
    3. Automatic or Explicit Buffering  
  