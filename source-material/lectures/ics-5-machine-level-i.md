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

#wip 27:09
