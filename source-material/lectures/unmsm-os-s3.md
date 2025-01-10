---
tags:
  - "#lecture-notes"
src-date: 2024-09-04
src-author: 
src-link:
---
# Operating Systems - Session 3

## Syscalls

- API != Web API
- The most important thing to care about is the syscall's function definition
- [POSIX](https://pubs.opengroup.org/onlinepubs/9799919799/): API for UNIX-based systems

![Pasted image 20240904145544](../../utilities/attachments/Pasted%20image%2020240904145544.png)

- The OS has a syscall table
- It's possible to add [custom syscalls](https://www.kernel.org/doc/html/latest/process/adding-syscalls.html)
- In UNIX, all communications between devices, files, and processes are abstracted to a set of syscalls: open, close, read, and write
- read and write are mediated by a kernel buffer
- pipes allow process communication using two file descriptors, one for reading and one for writing

## Threads

> A thread is a single execution sequence that represents a separately schedulable task.

![Pasted image 20240904155930](../../utilities/attachments/Pasted%20image%2020240904155930.png)

![Pasted image 20240904160247](../../utilities/attachments/Pasted%20image%2020240904160247.png)

Amdahl's Law: theoretical limits to the efficiency of process parallelization
$$
\text{speedup} \leq \dfrac{1}{S + \dfrac{1 - S}{N}}
$$
$S$: serial percentage of application
$N$: number of processors

- No such thing as threads in Linux, it's all processes and tasks
- fork and clone do similar things, you gotta be more careful with clone
- The [scheduler](scheduler%20(operating%20systems)) assigns processes to processors
- [Thread Control Block (TCB)](TCB))): thread state and metadata
- pthreads: POSIX library for threads
- IO bounds: concept related to tasks limited by i/o devices response time