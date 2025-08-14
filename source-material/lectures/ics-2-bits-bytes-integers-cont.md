---
tags:
  - "#lecture-notes"
src-date: 
src-author:
  - Randal E. Bryant
  - David R. O'Hallaron
src-link:
  - https://scs.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=526e6341-aa53-4107-8fa1-d13c0e92342e
---
# Bits, Bytes, and Integers (cont.)

## Integer arithmetic

### Addition

#### Unsigned

Implements modular arithmetic

$$
\text{UAdd}_w(u,v) = (u + v) \ \text{mod} \ 2^w
$$

```
operands:       u               1 1 1 1   ->   15
                v               0 1 1 0   ->    6
                                -------
true sum:       u + v         1 0 1 0 1   ->   21
(w+1 bits)                    ^ carry

discard carry:  UAdd_w(u, v)    0 1 0 1   ->    5 = 21 % 16
(w bits)
```

#### Two's Complement

```
operands:       u               1 1 1 1   ->   -1
                v               0 1 1 0   ->    6
                                -------
"true" sum:     u + v         1 0 1 0 1   ->   -11
(w+1 bits)                    ^ carry

discard carry:  UAdd_w(u, v)    0 1 0 1   ->    5 = -1 + 6 (wow!)
(w bits)
```

> It seems like magic because it is

The same hardware and algorithms used for addition work for either unsigned or two's complement

```c
int s, t;
int u = -1;
int v =  6;

s = (int) (
  (unsigned) u  // UMax 
+ (unsigned) v  // 6
);

t = u + v;

// s == t
```

- Negative overflow: Negative sum turns positive

```
          1 1 0 1   ->  -3
          1 0 1 0   ->  -6
          -------
        1 0 1 1 1   ->  -9
dropped ^
          0 1 1 1   ->   7
```

- Positive overflow: Positive sum turns negative

```
0 1 1 1   ->   7
0 1 0 1   ->   5
-------
1 1 0 0   ->  -4  
```

![](../../utilities/attachments/Pasted%20image%2020250812082244.png)

- Straight blue arrows: Sums within the range $-2^{w-1}$ to $2^{w-1} - 1$ ($w$-bit representable range) preserve their sign
- Red arrows: For sums that overflow the $w$-bit range (whether positively or negatively), the additional $w+1$ bit is dropped and the remaining bits are treated as another two's complement integer. This "flips" the resulting sign

### Multiplication

Similarly, the $w$ right-most bits are preserved, and the remaining ones are dropped.

#### Unsigned

Implements modular arithmetic

$$
\text{UMult}_w(u,v) = (u \cdot v) \ \text{mod} \ 2^w
$$

- Up to $2w$ bits
- True result range:
$$
\begin{align}
0 &\leq xy \leq \text{UMax}^2 \\
0 &\leq xy \leq (2^w - 1)^2 \\
0 &\leq xy \leq 2^{2w} - 2^{w+1} + 1
\end{align}
$$

```
                1 1 1 1   ->   15    UMax
                1 1 1 1   ->   15    UMax
                -------
        1 1 1 0 0 0 0 1   ->   225   max product
dropped ^ ^ ^ ^
                0 0 0 1   ->   1
```

#### Two's complement

- Up to $2w$ bits
- True result range:
$$
\begin{align}
\text{TMin} \cdot \text{TMax} &\leq xy \leq \text{TMin}^2 \\
(-2^{w-1}) (2^{w-1} - 1) &\leq xy \leq (-2^{w-1})^2 \\
-2^{2w-2} + 2^{w-1} &\leq xy \leq 2^{2w-2} \\
\end{align}
$$

```
                1 0 0 0   ->  -8    TMin
                0 1 1 1   ->   7    TMax
                -------
        1 1 0 0 1 0 0 0   ->  -56   min product
dropped ^ ^ ^ ^
                1 0 0 0   ->  -8
```

> [!note]
> The original lecture states that negative two's complement integers take up to $2w - 1$ bits. From what I've shown above, the minimum product for $w = 4$, which is $-8 \cdot 7 = -56$, takes 8 bits, not 7.
> 
> I could've messed up somewhere.

```
                1 0 0 0   ->  -8    TMin
                1 0 0 0   ->  -8    TMin
                -------
        0 1 0 0 0 0 0 0   ->   64   max product
dropped ^ ^ ^ ^
                0 0 0 0   ->   0
```

- Keeping product results exact would require to expand the word size
- "Arbitrary precision" arithmetic packages do this in software
- There are computer instructors which allow you to get the upper word of a multiplication

#### Power-of-2 multiply with left shift

$$
\begin{align}
      x &= \sum_{i=0}^{w-1} x_i \cdot 2^i \\
x \ll k &= \sum_{i=0}^{w-1} x_i \cdot 2^{i + k} \\
x \ll k &= 2^k \sum_{i=0}^{w-1} x_i \cdot 2^i \\
x \ll k &= 2^k \cdot x
\end{align}
$$

> [!note]
> The demonstration shown above assumes no truncation. Integer multiplication truncates the result anyway, making left shift practically equivalent to multiplication by a power of two.

#### Power-of-2 divide with right shift

$u \gg k$ (with logical shift) gives $\lfloor \dfrac{u}{2^k} \rfloor$ when $u$ is a multiple of $2^k$

**Signed case**: Use [arithmetic shift](ics-1-bits-bytes-integers.md) to preserve sign #wip

### Additive inverse

$$
-x = \sim x + 1
$$

> [!note]
> $\sim$: [binary negation](ics-1-bits-bytes-integers.md) 

## When should I use unsigned?

- *Don't* use without understanding implications
- *Do* use when performing modular arithmetic (e.g. encryption algorithms)
- *Do* use when using bits to represents sets

### Counting down with unsigned

The right loop condition should be `i < cnt`, which will turn false once `i` overflows from 0 to $\text{UMax}$. Remember that the C standard guarantees that unsigned addition will behave like modular arithmetic, thus $0 - 1 = \text{UMax}$.

```c
unsigned i;
for (i = cnt - 2; i < cnt; i--)
	a[i] += a[i+1];
```

Because of possible differences in the computer architecture, **you should not assume anything outside the C standard** (be conservative).

Even better:

```c
size_t i;
for (i = cnt - 2; i < cnt; i--)
	a[i] += a[i+1];
```

#wip

## Byte-oriented memory organization

- Memory: *conceptually* a big array of bytes
- Word size: nominal size of integer-valued data and addresses
- Addresses of successive words differ by 4 (32-bit) or 8 (64-bit)

### Byte ordering within word

- Big Endian: Least significant byte -> Highest address (Used on the Internet)
- Little Endian: Least significant byte -> Lowest address (Used almost anywhere else)

**Example**

- Variable `x` has 4-byte value of `0x01234567`
- `&x = 0x100`

Big Endian:

```
0x100  0x101  0x102  0x103
01     23     45     67
```

Little Endian:

```
0x100  0x101  0x102  0x103
67     45     23     01
```

> [!note]
> `%p` is a very useful C directive for printing pointers when debugging, as it prints out as many bytes as it takes for the particularly machine that is running on.
