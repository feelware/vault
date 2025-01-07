---
tags:
  - unmsm
  - wip
  - lecture-notes
src-date: 2014-08-21
src-author:
  - Thomas Anderson
  - Michael Dahlin
src-link: "[[source-material/textbooks/Operating_systems__principles_and_practice (Anderson og Dahlin)_text.pdf|Operating_systems__principles_and_practice (Anderson og Dahlin)_text]]"
---
# Operating Systems: Principle and Practice

## Chapter 1: Introduction

### What is an [[operating system]]?

An operating system plays three roles:

#### Referee

- Manage resources
- Isolate processes from each other
- Allow processes to communicate safely

#### Illusionist

- Abstract away hardware details
- Make up for certain hardware limitations

#### Glue

- Provide common APIs to apps, ensuring consistency and compatibility between them

### How to evaluate an OS?

#### Reliability & Availability

- A **reliable** OS does what's supposed to do
- An **available** OS works when needed
- An OS that crashes often and loses data is unreliable and unavailable
- An OS that crashes often but *doesn't* lose data is reliable but unavailable
- An OS that doesn't crash but allows key-loggers to run in the background is available but unreliable

#### Security

- **Security** means the computer can't be compromised by malicious actors
- **Privacy** means the computer's data can't be accessed by unauthorized users
- Although perfect security is impossible in practice, an OS design must *minimize* the attack surface
- An OS needs a **security policy** (access rules) and **enforcement** (mechanisms to enforce the rules)
- An error in enforcement allows to evade the policy
- An error in the policy allows access to things that shouldn't be accessed

#### Portability

- An OS must provide an abstraction that stays the same in spite of hardware changes
- The **Abstract Virtual Machine (AVM)** solves this by providing a standard interface between apps and the OS
- An AVM includes:
- **Application Programming Interface (API)**: List of function calls the OS provides
- Memory access model
- Which instructions can be legally executed
- The **Hardware Abstraction Layer (HAL)** is a module in the OS that hides the specifics of hardware implementations
- The HAL is much closer to the hardware than the AVM

#### Performance

- The OS design can greatly affect the application's perceived performance
- **Overhead**: Cost of implementing an abstraction
- **Efficiency**: Lack of overhead in an abstraction (inverse of overhead)
- **Fairness**: Whether resources distribution is equitable or according to certain priorities
- **Response time**: Time from request to response (individual)
- **Throughput**: Rate at which requests are processed (aggregate)
- Designs that improve response time don't necessarily improve throughput
- **Performance predictability**: Consistency of response time over time

#### Adoption

- **Network effect**: The value an OS provides is affected by factors outside its immediate control
- Making your OS compatible with existing apps increases its adoption
- Some companies make their OSes less compatible to increase adoption of their own software and hardware

### Past, Present, and Future of Operating Systems

#### Impact of technology trends

- Due to Moore's Law, computation has gotten really cheap
- We still face many OS design challenges from the past, and will continue to do so in the future

#### Early Operating Systems

- Early computers were really expensive to use
- As a result, early OSes were designed to minimize programmer error
- Early OSes were rustic, consisting mostly of common services like I/O

#### Multi-User Operating Systems

- In early systems, the processor remained idle while the user loaded a program
- **Batch operating systems** solved this:
- I/O devices are now able to load data without the processor's direct intervention (**Direct Memory Access (DMA)**)
- Once the device is done transferring data, it interrupts the processor
- The processor starts the next transfer and goes back to the previous program
- This approach evolved into **multitasking** by loading multiple programs into memory and allowing them to run when the processor is available

#### Time-sharing Operating Systems

- Time-sharing OS are optimized for user interaction rather than batch processing
- Every user input causes an interrupt, which is queued inside the OS
- After the interrupt, the current program fetches the event and processes it

#### Future Operating Systems

- Physical structure coordination, among other processes, could benefit greatly from being controlled by secure, reliable computers
- The future of OS design is conditioned by the future of hardware design

## Chapter 2: The Kernel Abstraction

The OS needs to restrict applications from doing certain things to ensure:
- Reliability: Neither apps nor users should crash the entire OS
- Security: Malicious apps shouldn't be able to modify the OS, this would allow them to circumvent other security enforcement measures
- Privacy: Apps shouldn't have read access to potentially sensitive data
- Fairness: Apps shouldn't be allowed to hoard computer resources

The [[kernel]], with full access to hardware, is responsible for restricting these apps.

![[utilities/attachments/Pasted image 20240901142243.png]]

A [[process (computing)|process]] is an instance of an application running with **restricted access** to hardware, which the kernel mediates.

### The process concept

- There can be multiple instances of the same program running on a computer. For every open process, the OS loads a copy of the running program in memory.
- The [[process control block]] (PCB) is a data structure that stores everything the OS needs to know about a certain process (location in memory, privileges, location of the executable image, etc).
- Most processes have multiple activities running in parallel. We're talking about [[thread|threads]].

### Dual-mode operation

- The processor is able to execute many sorts of instructions. Although some are relatively innocuous (like multiplying numbers), some others are *very* critical (writing to memory or disk, for instance) and pose a danger to other processes and even the OS.
- A *hypothetical* solution would be to analyze/simulate every instruction that comes from a process before actually executing it on bare metal. If a certain process is overstepping its bounds, we could just halt it.
- A more realistic approach to this idea is [[dual-mode operation]]: running kernel-issued instructions directly on hardware, while performing safety checks on every other instruction. A single bit in the status register indicates whether the current instruction comes from the kernel or a process.

There are multiple things the hardware must support in order to achieve dual-mode operation:

#### Privileged instructions

- Among other things, processes are forbidden from executing instructions that:
	- Change their privilege *directly* (without [[syscall|syscalls]]). Only the kernel is allowed to change the mode bit (See [[#Safe control transfer]]).
	- Allow them to access memory outside the bounds set *only* by the kernel (see [[#Memory protection]]).
	- Disable processor interrupts (see [[#Timer interrupts]]).
- On the other hand, the kernel must be allowed to do these, otherwise it wouldn't be able to do its job.
- If a process attempts to execute a privileged instruction, a **processor exception** will be triggered. The kernel handles these exceptions, usually by just halting such process.

#### Memory protection

- Since both the OS and the current processes need to be in memory at the same time, processes' memory access must be restricted to certain kernel-defined regions.
- Early OSes implemented memory protection using **base** and **bound** registers, which indicate the start and length of the current process' memory area, respectively.
- The processes, unable to access memory that isn't theirs, need the kernel to take care of their input and output operations.

![[utilities/attachments/Pasted image 20240903131941.png]]

- This approach has multiple limitations:
	- Neither the stack nor the heap can expand dynamically.
	- Processes can't share memory with each other.
	- Over time, physical memory starts to fragment, not leaving enough contiguous space to allocate processes.
- **Virtual addresses** abstract away physical addresses from processes, giving them the illusion of starting at address zero.
- Complex algorithms are used to translate virtual addresses to physical locations, allowing the OS to manage memory more efficiently.
- Imagine a simple program that assigns a random value to a static variable and waits a couple of seconds to print both the value and address of said variable. Running multiple instances of this program (in a modern OS) will show the same address but a different value on each instance.
- Evidently, each process has its own "sandbox" where all memory accesses happen in a virtual space. This renders processes unable to access memory that isn't theirs.

#### Timer interrupts

- The kernel needs to regain control periodically, regardless of what the current process is doing, so it can decide whether to keep running said process, pay attention to other processes, respond to user input, among other things.
- A hardware timer is responsible for interrupting the processor every ten milliseconds or so.

### Safe control transfer

#### User to kernel

- **Hardware interrupts** (asynchronous signals sent to the processor by external devices, like I/O devices, the timer clock or even other processors)
- **Processor exceptions** (illegal conditions in user programs that cause the CPU to halt such process)
- **Syscalls**

#### Kernel to user

- Creating a new process
- Resuming a process' execution (after an exception, interrupt or syscall)
- Switching to a different process (like pintos' context switches)
- User-level upcalls #wip

#wip

## Chapter 3: The Programming Interface

- There are many services the operating system can provide to applications: some of the most important, yet surprisingly minimal to implement, are process management and input/output.
- Whether we implement these services as user-level apps, user-level libraries, or part of the kernel through syscalls, is a matter of balancing:
	- Security: The kernel must implement resource management and protection (see [[#Chapter 2 The Kernel Abstraction]])
	- Flexibility: Allow applications and hardware to evolve independently by exposing a mostly transparent interface.
	- Reliability: A bug in the kernel can be fatal. As seen in [[#Chapter 2 The Kernel Abstraction|Chapter 2]], the hardware trusts the kernel not to crash the entire system. The least responsibility we give to the kernel, the more reliable the system will be. 
	- Performance: On the other hand, delegating too many OS tasks to user processes can slow things down due to excessive syscalls, which tend to be expensive.

### Process management

- Early OSes were forced to manage processes at kernel-level. Nowadays, many user-level applications can manage other processes. The shell is one of such applications.

#wip 

## Chapter 4: Concurrency and Threads

- Threads are pieces of code written in **sequence** but executed in **parallel**. They give the illusion of infinite processors by multiplexing the current tasks on a finite number of processors, running a small portion of these tasks at the time.
- 