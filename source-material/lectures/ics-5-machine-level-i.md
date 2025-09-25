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

| C       | ASM      | Explanation                                                                                                                     |
| ------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- |
| `t`     | `%rax`   | Register `%rax` holds the value of `t`                                                                                          |
| `dest`  | `%rbx`   | Register `%rbx` holds the value of `dest`, which is a memory address                                                            |
| `*dest` | `(%rbx)` | Surrounding a register by parentheses accesses the memory at the "index" provided by register. In short, `(%rbx)` = `Mem[%rbx]` |

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

## Moving data

```
movq Source, Dest
```

Can move value of:
- Constant
	- To register: `movq $0x69, %rax`
	- To memory: `movq $0x69, (%rax)`
- Register
	- To memory: `movq %rax, (%rbx)`
	- To another register: `movq %rax, %rbx`
- Memory
	- To register: `movq (%rax), %rbx`

Not possible to move from memory to memory (with a single instruction)

### Simple memory addressing modes

#### Normal `(R)`

- Equivalent to pointer dereferencing in C
- Example: `movq (%rcx), %rax`
- Equivalent to: `a = *c`

#### Displacement `D(R)`

- Register `R` specifies start of memory region
- Constant `D` specifies offset
- Example: `movq 8(%rcx), %rax`
- Equivalent to: `a = *(c + 8)`

### C Example

```c
void swap(long *xp, long *yp) {
	long t0 = *xp;
	long t1 = *yp;
	*xp = t1;
	*yp = t0;
}
```

- In x86-64, the arguments are copied to specific registers
	- First argument: `%rdi`
	- Second argument: `%rsi`

```asm
swap:
	movq (%rdi), %rax
	movq (%rsi), %rdx
	movq %rdx, (%rdi)
	movq %rax, (%rsi)
	ret
```

> [!note]
> - The "q" in `movq` makes reference to "quad" word (four times a word)
> - in x86-64 a word is 16 bits long, so a quad word is 64 bits long (or 8 bytes if you prefer)

### Complete memory addressing modes

- Assembly form: `D(Rb, Ri, S)`
- Equivalent to `Mem[Rb + Ri*S + D]`
	- `Rb`: base register
	- `Ri`: index register (`%rsp` not allowed)
	- `S`: constant index scale (1, 2, 4, or 8)
	- `D`: constant offset (1, 2, 4, or 8)
- "Natural way to implement array indexing"

#### Example

`movq %rax, 0(%rbx, %rdx, 4)`

- `Rb` = `0x69`
- `Ri` = `0x3`
- `S` = 4
- `D` = 0
- Destination: `0x69 + 0x3 * 4 + 0` = `0x6d`

![](../../utilities/attachments/Pasted%20image%2020250925161354.png)

#### Special cases

- No index scale: `D(Rb, Ri)` = `Mem[Rb + Ri + D]`
- No constant offset: `(Rb, Ri, S)` = `Mem[Rb + Ri*S]`
- No index scale nor constant offset: `(Rb, Ri)` = `Mem[Rb + Ri]`
