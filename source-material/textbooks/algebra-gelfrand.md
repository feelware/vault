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

```js
(1 * 10**20)/7: 	14285714285714287000
(2 * 10**20)/7: 	28571428571428573000
(3 * 10**20)/7: 	42857142857142850000
(4 * 10**20)/7: 	57142857142857150000
(5 * 10**20)/7: 	71428571428571430000
(6 * 10**20)/7: 	85714285714285700000
(7 * 10**20)/7: 	100000000000000000000
(8 * 10**20)/7: 	114285714285714300000
(9 * 10**20)/7: 	128571428571428570000
(10 * 10**20)/7: 	142857142857142860000
(11 * 10**20)/7: 	157142857142857140000
(12 * 10**20)/7: 	171428571428571400000
(13 * 10**20)/7: 	185714285714285720000
(14 * 10**20)/7: 	200000000000000000000
(15 * 10**20)/7: 	214285714285714280000
(16 * 10**20)/7: 	228571428571428600000
(17 * 10**20)/7: 	242857142857142860000
(18 * 10**20)/7: 	257142857142857140000
(19 * 10**20)/7: 	271428571428571400000
(20 * 10**20)/7: 	285714285714285720000
(21 * 10**20)/7: 	300000000000000000000
```

