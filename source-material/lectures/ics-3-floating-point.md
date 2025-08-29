---
tags:
  - "#lecture-notes"
src-date: 
src-author:
  - Randal E. Bryant
  - David R. O'Hallaron
src-link:
  - https://scs.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=8dd08ed5-7688-4b34-937f-201b909f61c7
---
# Floating Point

## Value formula

$$
v = (-1)^s \cdot 2^E \cdot M
$$

Remember that `exp` is not equal to $E$, it only encodes it. For [normalized](#Normalized) numbers, `exp` is equal to $E$ plus some [bias](#Bias%20formula). For [denormalized](#Denormalized) numbers, `exp` is equal to all zeroes.

Similarly, `frac` is not equal to $M$. `frac` only stores the part that comes after the decimal dot. Whether it's 0 or 1 that comes before the dot, depends on whether the number is normalized or denormalized.

## Bias formula

Let $l$ be the length of the `exp` field (in bits)

$$
\text{Bias} = 2^{l-1} - 1
$$

## Example: 6-bit IEEE-like format

```
_   _ _ _   _ _
s   exp     frac
1   3       2
```

In this case, since the length of `exp` is equal to 3, the bias is equal to $2^{3-1} - 1 = 3$

### Dynamic range

#### Normalized

- $M = 1.$`frac`
- `exp` is always different from `000`
- $E = \text{Exp} - \text{Bias} = \text{Exp} - 3$

> [!note]
> $\text{Exp}$ is the unsigned base-10 representation of `exp`

| $s$ | `exp` | $E$              | $2^E$          | `frac` | $M$                                                       | $v$                                                             |
| --- | ----- | ---------------- | -------------- | ------ | --------------------------------------------------------- | --------------------------------------------------------------- |
| `0` | `001` | $001_2 - 3 = -2$ | $\dfrac{1}{4}$ | `00`   | $1.00_2 = 1 + \dfrac{0}{2} + \dfrac{0}{4} = \dfrac{4}{4}$ | $(-1)^0 \cdot \dfrac{1}{4} \cdot \dfrac{4}{4} = \dfrac{4}{16}$  |
| `0` | `001` | $001_2 - 3 = -2$ | $\dfrac{1}{4}$ | `01`   | $1.01_2 = 1 + \dfrac{0}{2} + \dfrac{1}{4} = \dfrac{5}{4}$ | $(-1)^0 \cdot \dfrac{1}{4} \cdot \dfrac{5}{4} = \dfrac{5}{16}$  |
| `0` | `001` | $001_2 - 3 = -2$ | $\dfrac{1}{4}$ | `10`   | $1.10_2 = 1 + \dfrac{1}{2} + \dfrac{0}{4} = \dfrac{6}{4}$ | $(-1)^0 \cdot \dfrac{1}{4} \cdot \dfrac{6}{4} = \dfrac{6}{16}$  |
| `0` | `001` | $001_2 - 3 = -2$ | $\dfrac{1}{4}$ | `11`   | $1.11_2 = 1 + \dfrac{1}{2} + \dfrac{1}{4} = \dfrac{7}{4}$ | $(-1)^0 \cdot \dfrac{1}{4} \cdot \dfrac{7}{4} = \dfrac{7}{16}$  |
| `0` | `010` | $010_2 - 3 = -1$ | $\dfrac{1}{2}$ | `00`   | $1.00_2 = 1 + \dfrac{0}{2} + \dfrac{0}{4} = \dfrac{4}{4}$ | $(-1)^0 \cdot \dfrac{1}{2} \cdot \dfrac{4}{4} = \dfrac{8}{16}$  |
| `0` | `010` | $010_2 - 3 = -1$ | $\dfrac{1}{2}$ | `01`   | $1.01_2 = 1 + \dfrac{0}{2} + \dfrac{1}{4} = \dfrac{5}{4}$ | $(-1)^0 \cdot \dfrac{1}{2} \cdot \dfrac{5}{4} = \dfrac{10}{16}$ |
| `0` | `010` | $010_2 - 3 = -1$ | $\dfrac{1}{2}$ | `10`   | $1.10_2 = 1 + \dfrac{1}{2} + \dfrac{0}{4} = \dfrac{6}{4}$ | $(-1)^0 \cdot \dfrac{1}{2} \cdot \dfrac{6}{4} = \dfrac{12}{16}$ |
| `0` | `010` | $010_2 - 3 = -1$ | $\dfrac{1}{2}$ | `11`   | $1.11_2 = 1 + \dfrac{1}{2} + \dfrac{1}{4} = \dfrac{7}{4}$ | $(-1)^0 \cdot \dfrac{1}{2} \cdot \dfrac{7}{4} = \dfrac{14}{16}$ |
| ... |       |                  |                |        |                                                           |                                                                 |
| `0` | `111` | $111_2 - 3 = 4$  | 16             | `00`   | $1.00_2 = 1 + \dfrac{0}{2} + \dfrac{0}{4} = \dfrac{4}{4}$ | $(-1)^0 \cdot 16 \cdot \dfrac{4}{4} = 16$                       |
| `0` | `111` | $111_2 - 3 = 4$  | 16             | `01`   | $1.01_2 = 1 + \dfrac{0}{2} + \dfrac{1}{4} = \dfrac{5}{4}$ | $(-1)^0 \cdot 16 \cdot \dfrac{5}{4} = 20$                       |
| `0` | `111` | $111_2 - 3 = 4$  | 16             | `10`   | $1.10_2 = 1 + \dfrac{1}{2} + \dfrac{0}{4} = \dfrac{6}{4}$ | $(-1)^0 \cdot 16 \cdot \dfrac{6}{4} = 24$                       |
| `0` | `111` | $111_2 - 3 = 4$  | 16             | `11`   | $1.11_2 = 1 + \dfrac{1}{2} + \dfrac{1}{4} = \dfrac{7}{4}$ | $(-1)^0 \cdot 16 \cdot \dfrac{7}{4} = 28$                       |

> [!note]
> The values for $s = 1$ are the same as the ones for $s = 0$, just negative.

Notice how the distance between values of $v$  turns exponentially bigger as $E$ increases

- For $E = -2$, the distance is 1/16
- For $E = -1$, the distance is 1/8
- Moving all the way up to $E = 4$, the distance is 4

> Every time you increase the exponent by 1, the numbers are spaced twice as far apart as the numbers represented by the previous exponent.

#### Denormalized

- $M = 0.$`frac`
- `exp` is always `000`
- $E$ is fixed to $1 - \text{Bias} = 1 - 3 = -2$

| $s$ | `exp` | $E$ | $2^E$          | `frac` | $M$                                                   | $v$                                                             |
| --- | ----- | --- | -------------- | ------ | ----------------------------------------------------- | --------------------------------------------------------------- |
| `0` | `000` | -2  | $\dfrac{1}{4}$ | `00`   | $0.00_2 = \dfrac{0}{2} + \dfrac{0}{4} = \dfrac{0}{4}$ | $(-1)^0 \cdot \dfrac{1}{4} \cdot \dfrac{0}{4} = \dfrac{0}{16}$  |
| `0` | `000` | -2  | $\dfrac{1}{4}$ | `01`   | $0.01_2 = \dfrac{0}{2} + \dfrac{1}{4} = \dfrac{1}{4}$ | $(-1)^0 \cdot \dfrac{1}{4} \cdot  \dfrac{1}{4} = \dfrac{1}{16}$ |
| `0` | `000` | -2  | $\dfrac{1}{4}$ | `10`   | $0.10_2 = \dfrac{1}{2} + \dfrac{0}{4} = \dfrac{2}{4}$ | $(-1)^0 \cdot \dfrac{1}{4} \cdot  \dfrac{2}{4} = \dfrac{2}{16}$ |
| `0` | `000` | -2  | $\dfrac{1}{4}$ | `11`   | $0.11_2 = \dfrac{1}{2} + \dfrac{1}{4} = \dfrac{3}{4}$ | $(-1)^0 \cdot \dfrac{1}{4} \cdot  \dfrac{3}{4} = \dfrac{3}{16}$ |

> [!note]
> Same as before, the values for $s = 1$ are the same as the ones for $s = 0$, just negative.
