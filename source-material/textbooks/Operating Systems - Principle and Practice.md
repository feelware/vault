---
tags:
  - unmsm
  - wip
  - lecture-notes
src-date: 2014-08-21
src-author:
  - Thomas Anderson
  - Michael Dahlin
src-link: "[[os-principles-practice.pdf]]"
---
# Operating Systems: Principle and Practice
---

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

---

## Chapter 2: The Kernel Abstraction

The OS needs to restrict applications from doing certain things to ensure:
- Reliability: Neither apps nor users should crash the entire OS
- Security: Malicious apps shouldn't be able to modify the OS, this would allow them to circumvent other security enforcement measures
- Privacy: Apps shouldn't have read access to potentially sensitive data
- Fairness: Apps shouldn't be allowed to hoard computer resources

The [[kernel]], with full access to hardware, is responsible for restricting these apps.

![[Pasted image 20240901142243.png]]

A [[process (computing)|process]] is an instance of an application running with **restricted access** to hardware, which the kernel mediates with assistance from the hardware.

### The Process Concept

- There can be multiple instances of the same program running on a computer. For every open process, the OS loads a copy (sorta) of the running program in memory.
- The [[process control block]] (PCB) is a data structure that stores everything the OS needs to know about a certain process (location in memory, privileges, location of the executable image, etc).
- Most processes have multiple activities running in parallel. We're talking about [[thread|threads]].

### Dual-mode operation

- The processor is able to execute many sorts of instructions. Although some are relatively innocuous (like multiplying numbers), some others are *very* critical (writing to memory or disk, for instance) and pose a danger to other processes or even the OS.
- A *hypothetical* solution would be to analyze/simulate every instruction in an user process before actually executing it on bare metal. If a certain process is overstepping its bounds, we could just halt it.
- A more realistic approach to this idea is [[dual-mode operation]]: running kernel-issued instructions directly on hardware, while performing safety checks on every other instruction.
- A single bit in the status register indicates whether the current instruction comes from the kernel or an user-level process.

There are multiple things the hardware must provide in order to achieve dual-mode operation:

#### Privileged instructions

- Processes must be forbidden from:
	- Changing their privilege *directly* (without [[syscall|syscalls]]). Protection measures are useless if perpetrators can get around them.
	- Changing their memory-access bounds, otherwise they'd be able to corrupt other processes or even the OS.
	- Disabling processor interrupts
- On the other hand, the kernel must be *allowed* to do these, otherwise it wouldn't be able to do its job.
- If a process attempts to execute a privileged instruction, a **processor exception** will be triggered. The kernel handles these exceptions, usually by just halting the perpetrating process.

#### Memory protection

- Both the OS and the current processes have tasks that require them to be in memory, at the same time.