---
tags:
  - "#lecture-notes"
src-date:
src-author:
  - Randal E. Bryant
  - David R. O'Hallaron
src-link:
  - https://scs.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=6e410255-3858-4e85-89c7-812c5845d197
---
# Machine Level Programming I: Basics

## Intel x86 Processors

- Desktop/Server Standard
- Backwards compatible (up to 8086)
- Lots of instructions, but only a few used by `gcc` to make Linux programs

### Evolution

- 2006: First multi-core Intel processor (Core 2)
	- Motivation: Single-score approach reached a power-consumption limit (100 Watt)
	
> When you put a lot of computers in a room, turns out power is the biggest issue you have to deal with

## Definitions

- **Architecture (ISA)**: Abstraction. Target of a compiler
- **Microarchitecture**: Implementation of architecture

## Assembly/Machine Code View

### Virtual memory

Fiction made in collaboration between hardware and OS. Each process views the entire memory as belonging to itself entirely, when in reality it's shared among multiple processes

### Cache

- Hidden from programmer (can't be manipulated with CPU instructions)

> It is automatically loaded with recent stuff, and the *only* thing that will look different is: if you access that memory it will go faster than it would if it hadn't been cached

## Assembly characteristics

### Data types

- "Integers": 1, 2, 4, or 8 bytes (used for both data and pointers)
- Floating point: 4, 8, or 10 bytes

### Operations

- Perform arithmetic operations on data from registers or memory
- Transfer data between memory and registers
- Transfer control (unconditional and conditional jumps)

## Example

### C

```c
*dest = t;
```

### Assembly

```asm
movq %rax, (%rbx)
```

| C       | ASM      | Explanation                                                                                                                        |
| ------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `t`     | `%rax`   | Register `%rax` holds the value of `t`                                                                                             |
| `dest`  | `%rbx`   | Register `%rbx` holds the value of `dest`, which is a memory address                                                               |
| `*dest` | `(%rbx)` | Surrounding a register by parentheses accesses the memory at the "index" provided by register. In short, `(%rbx)` = `Memory[%rbx]` |

### Object Code

```
48 89 03
```

## x86-64 Integer Registers

- Registers starting with `r` are 64-bit long (full register)
	- Example: `%rax`
	- Used for `long int`
- Registers starting with `e` are 32-bit long (lower-order 32 bits)
	- Example: `%eax`
	- Used for `int`
- You can also reference lower-order 16, 4, 2, and 1 bytes

- IA32: only 8 registers:
	- General purpose: `%eax`, `%ebx`, `%ecx`, `%edx`, `%esi`, `%edi`
	- `%esp`, `%ebp`
- x86-64 doubles the amount of registers
	- New ones have numbers in their names: `%r8`, `%r9`, ... `%r15`
	- Nowadays, most register names are legacy and have nothing to do with their current purpose, except for `%rsp` (stack pointer)

#wip left at 53:16
