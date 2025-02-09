---
tags:
  - "#textbook-notes"
  - wip
src-date: 1993-09-17
src-author:
  - Alexander Shen
  - Israel Gelfand
src-link: "[[pdf/algebra-shen-gelfand.pdf|algebra-gelfand]]"
---
# Algebra

## 3

> [!problem]-
> A boy claims that he can multiply any three-digit number by 1001 instantly. If his classmate says to him 715 he gives the answer immediately. Compute this answer and explain the boy’s secret.

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

> [!problem]-
> Multiply 101010101 by 57.

5757575757

## 5

> [!problem]-
> Multiply 10001 by 1020304050.

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

> [!problem]-
> Multiply 11111 by 1111.

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

> [!problem]-
> Divide 123123123 by 123 (Check your answer by multiplication!)

$$
\dfrac{123123123}{123} = \dfrac{123(10^6 + 10^3 + 1)}{123} = 10^6 + 10^3 + 1 = 1001001
$$

## 9

> [!problem]-
> Can you predict the remainder when 111...1 (100 ones) is divided by 1111111?

#wip 

## 10

> [!problem]-
> Divide 1000...0 (20 zeros) by 7.

$$
\begin{align*}
\dfrac{10^{20}}{7} = 10^{20} \left(\dfrac{1}{7}\right) = 10^{20} \cdot 0.\overline{142857} = 14285714285714285714.\overline{285714}
\end{align*}
$$

## 11

> [!problem]-
> While solving the two preceding problems you may have discovered that quotient digits (and remainders) became periodic:
> 
> ![](../../utilities/attachments/Pasted%20image%2020250111125559.png)
> 
> Is it just a coincidence, or will this pattern repeat?

As shown above, $10^{20}$ divided by 7 is equal to $10^{20}$ times $1/7$.

Since $1/7$ results in a repeating decimal ($0.\overline{142857}$) and multiplying a decimal by $10^n$ simply shifts the decimal $n$ times to the right ($n \geq 0$), $10^{20}$ times $1/7$ will also result in a repeating decimal.

## 12

> [!problem]-
> Divide 2000...000 (20 zeros), 3000...000 (20 zeros), 4000...000 (20 zeros), etc. by 7. Compare the answers you get and explain what you see.

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

## 13

> [!problem]-
> A multiplication fan may enjoy the following problem:
> 
> Multiply 142857 by 1, 2, 3, 4, 5, 6, 7, and look at the results. (It is easy to memorize these results and become a famous number cruncher who is able to multiply a random number, for example, 142857, by almost any digit!)

$$
\begin{align*}
1 \cdot 142857 = 142857 \\
2 \cdot 142857 = 285714 \\
3 \cdot 142857 = 428571 \\
4 \cdot 142857 = 571428 \\
5 \cdot 142857 = 714285 \\
6 \cdot 142857 = 857142 \\
7 \cdot 142857 = 999999 \\
\end{align*}
$$

Again, we notice that the same sequence repeats with different offsets. This is because [142857 is a cyclic number](https://www.wikiwand.com/en/articles/142857#Cyclic_number). 

## 14

> [!problem]-
> Try to invent similar tricks based on the division of 1000... 0 by other numbers instead of 7.

#wip

## 15

> [!problem]-
> Find a generating rule, and write five or ten more lines:
> 
> $$
> \begin{align*}
>    0\\
>    1\\
>   10\\
>   11\\
>  100\\
>  101\\
>  110\\
>  111\\
> 1000\\
> 1001\\
> 1010\\
> 1011\\
> 1100\\
> ...
> \end{align*}
> $$

These are just the natural numbers in base 2

$$
\begin{align*}
  ...\\
 1101\\
 1110\\
 1111\\
10000\\
10001\\
10010\\
10011\\
10100\\
10101\\
10110
\end{align*}
$$

#wip

## 16

> [!problem]-
> You have weights of 1, 2, 4, 8, and 16 grams. Show that it is possible to get any weight from 0 to 31 grams using the following table ("+" means "the weight is used", "—" means "not used"):
> 
> ![](../../utilities/attachments/Pasted%20image%2020250113143546.png)
> 
> We can replace "—" by 0 and "+" by 1 (column B) and omit the leading zeros (column C). Then we get the same result as in the preceding problem.

#wip 

## 17

> [!problem]-
> This table is called a conversion table between decimal and binary number systems:
> 
> | Decimal | Binary |
> | ------- | ------ |
> | 0       | 0      |
> | 1       | 1      |
> | 2       | 10     |
> | 3       | 11     |
> | 4       | 100    |
> | 5       | 101    |
> | 6       | 110    |
> | 7       | 111    |
> | 8       | 1000   |
> | 9       | 1001   |
> | 10      | 1010   |
> | 11      | 1011   |
> | 12      | 1100   |
> 
> What corresponds to 14 in the right column? What corresponds to 10000 in the left column?

14 to binary is 1110

```
14 |2
 0  7 |2
    1  3 |2
       1  1
```

10000 to decimal is 16

$$
16(1) + 8(0) + 4(0) + 2(0) + 1(0) = 16
$$

## 18

> [!problem]-
> How is 45 (decimal) written in the binary system?

32 is the greatest power of two less than 45. We *do* need a number 1 since 45 is odd. So far we have 33, 45 minus 33 is 12, 12 is 4 plus 8, which are powers of two, so the answer is 101101.

## 19

> [!problem]-
> What (decimal) number is written as 10101101 in binary?

$$
128(1) + 64(0) + 32(1) + 16(0) + 8(1) + 4(1) + 2(0) + 1(1) = 173
$$

## 20

> [!problem]-
> Try the usual addition method in binary version:
> 
> ```
> 1010 + 101  = ?
> 1111 + 1    = ?
> 1011 + 1    = ?
> 1111 + 1111 = ?
> ```
> 
> Check your answers, converting all the numbers (the numbers being added and the sums) into the decimal system.

```
1010 -> 10
 101 ->  5
----
1111 -> 15
```

```
 1111 -> 15
    1 ->  1
-----
10000 -> 16
```

```
1011 -> 11
   1 ->  1
----
1100 -> 12
```

```
 1111 -> 15
 1111 -> 15
-----
11110 -> 30
```

## 21

> [!problem]-
> Try the usual subtraction algorithm in its binary version:
> 
> ```
> 1101 - 101 = ?
>  110 - 1   = ?
> 1000 - 1   = ?
> ```

```
1101 -> 13
 101 ->  5
---- 
1000 ->  8
```

```
101 -> 6
  1 -> 1
---
101 -> 5
```

```
1000 -> 8
   1 -> 1
----
 111 -> 7
```

Check your answers, converting all the numbers into the decimal system.

## 22

> [!problem]-
> Now try to multiply 1101 and 1010 (in binary):
> 
> ```
> 1101
> 1010
> ----
> ????
> ```
> 
> Check your answers, converting all the numbers into the decimal system.

```
    1101 ->  13
    1010 ->  10
    ----
   1101
 1101
--------
10000010 -> 130
```

## 23

> [!problem]-
> Divide 11011 (binary) by 101 (binary) using the ordinary method. Check your result, converting all numbers into the decimal system.

```
11011 |101
101    101
---
  11
   0
  --
  111
  101
  ---
   10
```

```
27 |5
25  5
--
 2
```

## 24

> [!problem]-
> In the decimal system the fraction 1/3 is written as 0.333... What happens with 1/3 in the binary system?

```
1 |11
0  0.01
-
10
 0
--
100
 11
---
  1
```

The remainder circles back to 1, so the sequence "01" will repeat forever (0.010101...)

> [!note]
> - Commutative law: Order of terms doesn't affect result
> - Associative law: Order of operations doesn't affect result

## 28

> [!problem]-
> Add 899 + 1343 + 101.

899 + 1343 + 101 = (899 + 101) + 1343 = 1000 + 1343 = 2343
