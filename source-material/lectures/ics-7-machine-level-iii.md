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
# Machine Level Programming II: Procedures

Remember, the stack "grows" downwards.

## Passing control

- `callq` instruction implicitly does the following:
	- decrement `%rsp` (stack pointer) by 8
	- write return address (address adjacent to call) to the top of stack
	- change `%rip` (program counter) to address embedded in call (start of function)
- `retq` undoes the previous steps
	- read top of the stack, which is assumed to have the return address
	- increase `%rsp` by 8
	- change `%rip` to return address

#wip 22:49
