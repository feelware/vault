---
tags:
  - "#lecture-notes"
src-date: 
src-author:
  - Randal E. Bryant
  - David R. O'Hallaron
src-link:
  - https://youtube.com/playlist?list=PLyboo2CCDSWnhzzzzDQ3OBPrRiIjl-aIE
  - https://csapp.cs.cmu.edu/3e/labs.html
---
# Bits, Bytes, and Integers

Fractions can also be represented in binary

```
...  2^2  2^1  2^0  .  2^-1  2^-2  ...
     4    2    1       1/2   1/4
```

> [!NOTE]
> You'll get pretty good at converting hex to binary

64-bit machine = 64-bit addresses

## Bit-Level Operations in C

- Apply to any "integral" data type (long, int, short, char, unsigned)
- View arguments as bit vectors, operating on one bit at a time (bit-wise)

**Examples**

- `~0xC8` = `0x37`

```
~ 11001000
  --------
= 00110111
```

- `0xC8 & 0xB8` = `0x88`

```
  11001000  
& 10111000 
  -------- 
= 10001000
```

- `0xC8 | 0xB8` = `0xF8`

```
  11001000  
| 10111000 
  -------- 
= 11111000
```

## Contrast: Logic Operations in C

> [!NOTE]
> It's a common error for programmers to mix up `&&` for `&`, or `||` for `|`

> The "double" ones (like `||`) are *not* "thinking" about bit-wise operations (like `|` does), they're thinking about something that's either true or false.

- 0 is false, *anything* else is true
- always return 0 or 1
- **early termination** #wip

**Examples**

- `!0xC8` = `0x00`
- `!0x00` = `0x01`
- `!!0xC8` = `!0x00` = `0x01`
- `0xC8 && 0xB8` = `0x01`
- `0xC8 || 0xB8` = `0x01`

## Shift Operations

```
x << y
x >> y
```

Shift the number `x`, either to the left or right, `y` positions 

### Left shift

Leftmost bits are lost. Right side is *always* filled with zeroes

```
x           |01100010
x << 3   011|00010    <-
             00010000
         ---      ---
        lost      new
```

### Right shift

Rightmost bits are lost. What happens to the left side depends on the type

#### Logical shift

Left side is filled with zeroes, just as left shift does

```
x        01100010|
x >> 3      01100|010 ->
         00001100
         ---      ---
         new      lost
```

#### Arithmetic shift

Left side is filled with whatever value the leftmost bit (MSB) originally had

```
x        10100010|
x >> 3      10100|010 ->
         11110100
         ---      ---
         new      lost
```

If the original MSB is zero, it is effectively the same as logical shift

```
x        01100010|
x >> 3      01100|010 ->
         00001100
         ---      ---
         new      lost
```

> [!note]
> In most systems, shifting an 8-bit number `x` 8 positions returns `x` rather than 0. Shifting a negative number of positions, or a number of positions bigger than the word size, yields undefined behavior.

## Encoding Integers

### Unsigned

Given a number $X$ of size $w$
$$
B2U(X) = \sum_{i=0}^{w-1} x_i \cdot 2^i
$$
where $x_i$ can be either 0 or 1

> [!example]
> given $w=4$
> 
> | $i$   | 3   | 2   | 1   | 0   |
> | ----- | --- | --- | --- | --- |
> | $2^i$ | 8   | 4   | 2   | 1   |
> 
> `0xf = 8 + 4 + 2 + 1 = 15`

> [!note] Numeric ranges
> - UMin: 0 (000...0)
> - UMax: $2^w - 1$ (111...1)

### Two's Complement

MSB (biggest absolute value of $2^i$) is negative (also called sign bit)

$$
B2T(X) = -x_{w_1} \cdot 2^{w-1} + \sum_{i=0}^{w-2} x_i \cdot 2^i
$$

> [!example]
> given $w=4$
> 
> | $i$   | 3   | 2   | 1   | 0   |
> | ----- | --- | --- | --- | --- |
> | $\pm 2^i$ | -8   | 4   | 2   | 1   |
> 
> `0xf = -8 + 4 + 2 + 1 = -1`

> [!note] Numeric ranges
> - TMin: $-2^{w-1}$ (100...0)
> - TMax: $2^{w-1} - 1$ (011...1)

### Range comparison

Given $w=16$ (2 bytes)

|      | Decimal | Hex  | Binary                |
| ---- | ------- | ---- | --------------------- |
| UMax | 65535   | FFFF | `1111 1111 1111 1111` |
| TMax | 32767   | 7FFF | `0111 1111 1111 1111` |
| TMin | -32768  | 8000 | `1000 0000 0000 0000` |
| -1   | -1      | FFFF | `1111 1111 1111 1111` |
| 0    | 0       | 0000 | `0000 0000 0000 0000` |

## Unsigned & Signed Numeric Values

| $X$    | $B2U(X)$ | $B2T(X)$ |
| ------ | -------- | -------- |
| `0000` | 0        | 0        |
| `0001` | 1        | 1        |
| `0010` | 2        | 2        |
| `0011` | 3        | 3        |
| `0100` | 4        | 4        |
| `0101` | 5        | 5        |
| `0110` | 6        | 6        |
| `0111` | 7        | 7        |
| `1000` | 8        | -8       |
| `1001` | 9        | -7       |
| `1010` | 10       | -6       |
| `1011` | 11       | -5       |
| `1100` | 12       | -4       |
| `1101` | 13       | -3       |
| `1110` | 14       | -2       |
| `1111` | 15       | -1       |

> [!note]
> $B2U$ means binary to unsigned
> $B2T$ means binary to two's complement

> You'll often find cases where what used to be a very large number, because it was unsigned, all of a sudden becomes a negative number, because it's considered two's complement.

- For those where the MSB is zero, $B2U$ and $B2T$ are the same
- For those where the MSB is one, $B2U$ and $B2T$ will differ by $2^n$

## Mapping Between Signed & Unsigned

- These mappings **keep bit representations ($X$) and reinterpret**
- C performs these mappings
- The computer itself doesn't have a clue of whether something is signed or unsigned, it's all just bit patterns. Can lead to unexpected results (like adding or subtracting $2^w$)

### Two's Complement -> Unsigned ($T2U$)

$$
\begin{align}
x \rightarrow T2B &\rightarrow X \\
X \rightarrow B2U &\rightarrow ux \\
\end{align}
$$

### Unsigned -> Two's Complement ($U2T$)

$$
\begin{align}
ux \rightarrow U2B &\rightarrow X \\
X \rightarrow B2T &\rightarrow x \\
\end{align}
$$

## Signed vs. Unsigned in C

### Constants

- Considered signed integers by default
- Unsigned if suffix "U" is used (e.g. `0U`, `4294967259U`)

### Casting

Done using the [mappings](#Mapping%20Between%20Signed%20&%20Unsigned) mentioned above

- Can be explicit

```c
int tx, ty;
unsigned ux, uy;
tx = (int) ux;
uy = (unsigned) ty;
```

- Or implicit, via assignments and procedure calls

```c
tx = ux;   // ux -> U2T -> tx 
uy = ty;   // ty -> T2U -> uy
```

#### Expression evaluation

If there's a mix of unsigned and signed in a single expression (including comparisons), **signed values implicitly cast to unsigned**

Examples for $w = 32$
- UMax: 4294967296
- TMax: 2147483647
- TMin: -2147483648

| C1            | Relation | C2                | Evaluation | Result | Explanation                                                                             |
| ------------- | -------- | ----------------- | ---------- | ------ | --------------------------------------------------------------------------------------- |
| 0             | ==       | 0U*               | unsigned   | True   | Since there's an unsigned in the expression (0U), 0 (which is signed) casts to unsigned |
| -1            | <        | 0                 | signed     | True   | No casting                                                                              |
| -1            | >        | 0U                | unsigned   | True   | -1 is cast to unsigned, which is UMax, which is obviously bigger than 0                 |
| 2147483647    | >        | -2147483647 - 1   | signed     | True   | No casting. -214...7 - 1 is TMin, which is still "within range"                         |
| 2147483647U   | <        | -2147483647 - 1   | unsigned   | True   | -214...7 - 1, which is TMin, is cast to TMax + 1                                        |
| -1            | >        | -2                | signed     | True   | No casting                                                                              |
| (unsigned) -1 | >        | -2                | unsigned   | True   | -1 is cast to UMax, -2 is cast to UMax - 1                                              |
| 2147483647    | <        | 2147483648U       | unsigned   | True   | No casting                                                                              |
| 2147483647    | >        | (int) 2147483648U | signed     | True   | 214...8U, which is TMax + 1, is cast to TMin                                            |
