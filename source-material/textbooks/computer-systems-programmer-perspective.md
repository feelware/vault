---
tags:
  - "#textbook-notes"
  - wip
src-date: 
src-author:
  - Randal E. Bryant
  - David R. O'Hallaron
src-link:
  - "[[computer-systems-programmer-perspective]]"
---
# Computer Systems: A programmer's perspective

## A Tour of Computer Systems

### It Pays to Understand How Compilation Systems Work

- A basic understanding of compilers yields good coding decisions
- A lot of perplexing errors come from the linker

> For many years, **buffer overflow** vulnerabilities have accounted for many of the security holes in network and Internet servers. These vulnerabilities exist because too few programmers understand the need to carefully **restrict the quantity and forms of data they accept from untrusted sources**. A first step in learning secure programming is to understand the consequences of the way data and control information are stored on the program stack.

### Processors Read and Interpret Instructions Stored in Memory

> A processor *appears* to operate according to a very simple instruction execution model, defined by its **instruction set architecture**.

Instruction set architecture (ideal) != [Microarchitecture](https://en.wikipedia.org/wiki/Microarchitecture) (implementation)

### Caches matter

> The idea behind caching is that a system can get the effect of both a very large memory and a very fast one by exploiting **locality**, the tendency for programs to access data and code in localized regions.


