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

```asm
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

## Address Computation Instruction

Leverages the [complete memory addressing](#Complete%20memory%20addressing%20modes) mechanism we've just seen, giving developers **access to the result of that computation** rather than it just being used internally.

```asm
leaq (Rb, Ri, S), Dest
```

Equivalent to `Dest = Rb + Ri*S`

Used by the compiler to:
- Compute memory addresses of indexed arrays (e.g. `p = &x[i]`)
- Compute arithmetic expressions of the form `Rb + Ri*S`

## Some Arithmetic Operations

### One-operand

Form: `opr Dest`

| Format | Computation     | Notes   |
| ------ | --------------- | ------- |
| incq   | Dest = Dest + 1 |         |
| decq   | Dest = Dest - 1 |         |
| negq   | Dest = -Dest    |         |
| notq   | Dest = ~Dest    | Bitwise |

### Two-operand

While all of these instructions are of the form `opr Src, Dest`, the actual computation reverses that order. Think of it as "the destination being affected by some external value".

| Format | Computation        | Notes                                                                                  |
| ------ | ------------------ | -------------------------------------------------------------------------------------- |
| addq   | Dest = Dest + Src  |                                                                                        |
| subq   | Dest = Dest - Src  |                                                                                        |
| imulq  | Dest = Dest * Src  |                                                                                        |
| salq   | Dest = Dest << Src | Also called shlq<br>([there's no arithmetic left shift](ics-1-bits-bytes-integers.md)) |
| sarq   | Dest = Dest >> Src | Arithmetic                                                                             |
| shrq   | Dest = Dest >> Src | Logical                                                                                |
| xorq   | Dest = Dest ^ Src  |                                                                                        |
| andq   | Dest = Dest & Src  |                                                                                        |
| orq    | Dest = Dest \| Src |                                                                                        |

## Arithmetic Expression Example

```c
long arith (long x, long y, long z)
{
	long t1 = x + y;
	long t2 = z + t1;
	long t3 = x + 4;
	long t4 = y * 48;
	long t5 = t3 + t4;
	long rval = t2 * t5;
	return rval;
}
```

```
rval = t5              * t2
	   t5 = t3 + t4      t2 = z + t1
                                  t1 = x + y
       t5 = 4 + x + t4
                    t4 = (y + y * 2) << 4
```

- `x` -> `%rdi`
- `y` -> `%rsi`
- `z` -> `%rdx`

```asm
arith:
	leaq (%rsi, %rsi, 2), %rbx  # %rbx = (y + y * 2) = y * 3
	salq $4, %rbx               # %rbx = (y * 3) << 4 = t4
	leaq 4(%rdi, %rbx), %rbx    # %rbx = 4 + x + t4 = t5
	
	leaq (%rdi, %rsi), %rax     # %rax = x + y = t1
	addq %rdx, %rax             # %rax = z + t1 = t2
	
	imulq %rbx, %rax            # %rax = t5 * t2 = rval
	ret
```

> [!note] Prof. implementation
> ![](../../utilities/attachments/Pasted%20image%2020251023142525.png)
> He went for the t1 -> t2 pipeline first. Since he had already used `z`, he was free to reuse `%rdx`, in this case to store `%t4`. Something I wonder is why didn't he keep using `%rdx` to store `t5`, and instead went for a  new register (`%rcx`)
