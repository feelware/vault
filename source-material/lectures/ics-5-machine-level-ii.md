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
# Machine Level Programming II: Control

## Condition codes

- Condition flags are set as a side effect of arithmetic operations (except `leaq`)
- Examples:
	- `ZF` (result is zero)
	- `SF` (result is negative)
	- `CF` (unsigned overflow)
	- `OF` (signed overflow)
		- Negative overflow: result is positive but both operands are negative, meaning that **the true result is negative** but cannot be represented as such due to size limits
		- Positive overflow: the opposite, the result is negative but both operands are positive so **the true result is positive**
- Can be set explicitly using `cmp` (compare) and `test`, which set the condition flags according to the result of a certain operation (the actual result goes nowhere)

### Compare

- Form: `cmp Src1, Src2`
- Sets flags according to the result of `Src2 - Src1` (keep the order in mind)
- As the name suggests, it's used to compare two numbers

### Test

- Form: `test Src1, Src2`
- Sets flags according to the result of `Src1 & Src2`
- Useful to have one of the operands as a bit mask

## Reading condition codes

### `SetX` instructions

- Format: `setx Dest`
- Set low-order byte of `Dest` to 1 if a certain combination of flags is met, 0 otherwise
- Do not affect the other 7 bytes

Some examples:

| Operation | Condition (flags) | Description/purpose                                                                               |
| --------- | ----------------- | ------------------------------------------------------------------------------------------------- |
| sete      | ZF                | Result is zero,<br>compared values are equal                                                      |
| setne     | ~ZF               | Result is non-zero,<br>compared values are not equal                                              |
| sets      | SF                | Result is negative                                                                                |
| setns     | ~SF               | Result is non-negative                                                                            |
| setl      | (SF ^ OF)         | Less (Either the result is negative<br>or there has been [negative overflow](#Condition%20codes)) |
| setle     | (SF ^ OF) \| ZF   | Less or equal                                                                                     |
| setg      | ~(SF ^ OF) & ~ZF  | Greater                                                                                           |
| setge     | ~(SF ^ OF)        | Greater or equal                                                                                  |

#### C Example

```c
int gt (long x, long y)
{
	return x > y;
}
```

```asm
gt:
	cmp    %rsi, %rdi   # x - y
	setg   %al          # %al = (x - y > 0) ? 1 : 0
	movzbl %al, %eax    # zero-out rest of %rax
	ret
```

> Notice how I flipped the order. It says `%rsi` (which is `y`) and `%rdi` (which is `x`) [...] so that I'm thinking in the order that the actual comparison is made in

`movzbl` only really zeroes-out the 3 upper bytes of `%eax` (the lower 4 bytes of `%rax`). But due to a quirk of x86-64, **every operation whose result is 4-byte long will fill the upper 4 bytes with zeroes**. So all of the 7 remaining bytes are zeroed-out automatically.

Alternative:

```
gt:
	cmpq   %rdi, %rsi    # y - x
	setl   %al           # %al = (y - x < 0) ? 1 : 0
	movzbl %al, %eax
	ret
```

### Jump instructions

- Unconditional jump: `jmp`
- Conditional jumps' names are analogous to [`SetX` instructions](#`SetX`%20instructions)

#### Example

```c
long absdiff (long x, long y)
{
	long result;
	if (x > y)
		result = x - y;
	else
		result = y - x;
	return result;
}
```

```asm
absdiff:
	cmpq %rsi, %rdi   # x - y
	jg greater
	
	movq %rsi, %rax
	subq %rdi, %rax
	ret
.greater:
	movq %rdi, %rax
	subq %rsi, %rax
	ret
```

#### General Conditional Expression Translation (Using Branches)

C version

```c
val = Test ? Then_Expr : Else_Expr
```

`goto` version

```c
	nTest = !Test;
	if (nTest) goto Else;  // if inverse condition is met, skip Then
// Then
	val = Then_Expr;
	goto Done;             // skip Else
Else:
	val = Else_Expr;
Done:                      // merge branches
	// ...
```

### Conditional moves

Branches are very disruptive to [instruction pipelining](https://en.wikipedia.org/wiki/Instruction_pipelining). CPUs are generally good at [branch prediction](https://en.wikipedia.org/wiki/Branch_predictor), but in some cases these predictions won't be better than choosing at random (e.g. computing absolute values).

> About half the time, whatever you guess you're gonna guess wrong.

"Backtracking" from a wrong prediction takes many CPU instructions. #wip For simple computations, it's faster to compute both results and choose which one to keep based on condition flags.

GCC uses conditional moves a lot.

```asm
absdiff:
	movq %rdi, %rax
	subq %rsi, %rax   # %rax = x - y
	
	movq %rsi, %rdx
	subq %rdi, %rdx   # %rdx = y - x
	
	cmpq %
```
