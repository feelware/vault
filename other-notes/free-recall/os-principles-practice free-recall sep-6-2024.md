---
tags:
  - free-recall
src-link: "[Operating Systems - Principle and Practice](Operating%20Systems%20-%20Principle%20and%20Practice)"
---
- operating systems isolate processes in a way that doesn't allow them to corrupt or access sensitive information from other processes or the OS itself
- the processor has two modes: user-mode and kernel-mode, defined by a single bit in the flags register
- as long as the processor is in kernel mode, all instructions will be executed directly
- in user mode, the processor will check whether the instruction is legal or not
	- ¿does the instruction change the process's privilege or memory bounds?
	- ¿does the instruction read or write to disk without syscalls?
- if the instruction is illegal, an exception is raised, which the kernel handles

- processes don't have access to physical addresses of memory. instead, they use "virtual addresses", an abstract sandbox where all addresses are available to the process, a sort of illusion. the kernel, which is trusted, translates those virtual addresses to actual physical addresses
- 