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
