---
tags:
  - "#lecture-notes"
src-date:
src-author:
  - Randal E. Bryant
  - David R. O'Hallaron
src-link:
  - https://scs.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=fc93c499-8fc9-4652-9a99-711058054afb
---
# Machine Level Programming III: Procedures

Remember, the stack "grows" downwards.

## Passing control

- `callq` instruction implicitly does the following:
	- pushes return address to stack, which itself involves:
		- decrementing `%rsp` (stack pointer) by 8
		- writing return address (address adjacent to call) to the top of stack
	- changes `%rip` (program counter) to address embedded in call (start of function)
- `retq` undoes the previous steps
	- pops return address out of the stack, which involves:
		- reading top of the stack, which is assumed to have the return address
		- increasing `%rsp` by 8
	- changes `%rip` to return address

## Passing data

- First 6 (int) arguments are to be copied to predetermined registers.
- Further arguments need to be accessed through memory, though it's rare to have a function with more than 6 arguments

## Managing local data

- **Stack Frame**: Block of state (extra arguments, local variables) of current procedure
- `%rbp` and `%rsp` point at base and top of current stack frame, respectively
	- The base pointer is not used as much anymore (only when frame size can't be known in advance)
- Latest callee is the only active procedure, previous callers are "frozen"
- Space for stack frame is allocated on function call
	- Space is deallocated on return 

> [!note]
> return address is not stored in the callee's frame, but in the caller's (at the top of it, to be precise)

> It's important to set `%rsp` back to where it should be before returning

## Register Saving Conventions

- **Caller saved**: Caller is in charge of saving. It saves registers to its stack before the call and restores them after
- **Callee saved**: Callee is in charge of saving. It saves registers before using them and restores them before returning

By convention, some registers are caller-saved (`%rax`, 6 argument registers, `%r10`, and `%r11`), while others are callee-saved (`%rbx`, etc)

## Observations about recursion

#wip
