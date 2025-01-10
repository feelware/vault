---
tags:
  - "#textbook-notes"
  - wip
src-date: 1993-09-17
src-author:
  - Alexander Shen
  - Israel Gelfand
src-link: "[[algebra-gelfand.pdf]]"
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
