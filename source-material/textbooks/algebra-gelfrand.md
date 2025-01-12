---
tags:
  - "#textbook-notes"
  - wip
src-date: 1993-09-17
src-author:
  - Alexander Shen
  - Israel Gelfand
src-link: "[algebra-gelfand](pdf/algebra-gelfand.pdf)"
---
# Algebra

## 3

A boy claims that he can multiply any three-digit number by 1001 instantly. If his classmate says to him 715 he gives the answer immediately. Compute this answer and explain the boy’s secret.

**Solution**

1001 times 715 is 715715. The incremental left shift of each sub product yields a very convenient sum with no carries, as shown in the figure below.

```
  1001 (x)
   ABC
  ----
  C00C
 B00B
A00A
------
ABCABC
```

## 4

Multiply 101010101 by 57.

**Solution**

5757575757

## 5

Multiply 10001 by 1020304050.

**Solution**

$$
\begin{align*}
1020304050 \cdot 10001 &= 1020304050 \cdot 10000 + 1020304050 \\
                       &= 10203040500000 + 1020304050 \\
\end{align*}
$$

```
10203040500000 (+)
    1020304050
--------------
10204060804050
```

## 6

Multiply 11111 by 1111.

**Solution**

```
   11111 (x)
    1111
   -----
   11111
  11111
 11111
11111
--------
12344321
```

## 8

Divide 123123123 by 123 (Check your answer by multiplication!)

**Solution**

$$
\dfrac{123123123}{123} = \dfrac{123(10^6 + 10^3 + 1)}{123} = 10^6 + 10^3 + 1 = 1001001
$$

## 9

Can you predict the remainder when 111...1 (100 ones) is divided by 1111111?

**Solution**

#wip 

## 10

Divide 1000...0 (20 zeros) by 7.

**Solution**

$$
\begin{align*}
\dfrac{10^{20}}{7} = 10^{20} \left(\dfrac{1}{7}\right) = 10^{20} \cdot 0.\overline{142857} = 14285714285714285714.\overline{285714}
\end{align*}
$$

## 11

While solving the two preceding problems you may have discovered that quotient digits (and remainders) became periodic:

![](../../utilities/attachments/Pasted%20image%2020250111125559.png)

Is it just a coincidence, or will this pattern repeat?

**Solution**

As shown above, $10^{20}$ divided by 7 is equal to $10^{20}$ times $1/7$.

Since $1/7$ results in a repeating decimal ($0.\overline{142857}$) and multiplying a decimal by $10^n$ simply shifts the decimal $n$ times to the right ($n \geq 0$), $10^{20}$ times $1/7$ will also result in a repeating decimal.

## 12

Divide 2000...000 (20 zeros), 3000...000 (20 zeros), 4000...000 (20 zeros), etc. by 7. Compare the answers you get and explain what you see.

**Solution**

$$
\begin{align*}
\dfrac{1 \cdot 10^{20}}{7} = 14285714285714285714.\overline{285714} \\
\dfrac{2 \cdot 10^{20}}{7} = 28571428571428571428.\overline{571428} \\
\dfrac{3 \cdot 10^{20}}{7} = 42857142857142857142.\overline{857142} \\
\dfrac{4 \cdot 10^{20}}{7} = 57142857142857142857.\overline{142857} \\
\dfrac{5 \cdot 10^{20}}{7} = 71428571428571428571.\overline{428571} \\
\dfrac{6 \cdot 10^{20}}{7} = 85714285714285714285.\overline{714285} \\
\end{align*}
$$

It's the same sequence of repeating decimals with different offsets to the left. Taking the first sequence as a reference (142857), we can list the offset for each product:

| Factor | Sequence | Offset |
| ------ | -------- | ------ |
| 1      | 142857   | 0      |
| 2      | 285714   | 2      |
| 3      | 428571   | 1      |
| 4      | 571428   | 4      |
| 5      | 714285   | 5      |
| 6      | 857142   | 3      |
