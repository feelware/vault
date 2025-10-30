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
# Machine Level Programming IV: Data

- In C, adding $k$ to a pointer is equivalent to adding $k \cdot s$ to it in assembly, where $s$ is the size of the pointer's data type

## Understanding Pointers & Arrays

#wip

`An`

| Declaration    | Compiles? | Null? | Size |
| -------------- | --------- | ----- | ---- |
| `int A1[3]`    | Y         | N     | 12   |
| `int *A2[3]`   | Y         | N     | 24   |
| `int (*A3)[3]` |           |       | 8    |
| `int (*A4[3])` |           |       | 24   |

`*An`

| Declaration    | Compiles? | Null? | Size |
| -------------- | --------- | ----- | ---- |
| `int A1[3]`    | Y         | N     | 4    |
| `int *A2[3]`   | Y         | N     | 8    |
| `int (*A3)[3]` |           |       | 12   |
| `int (*A4[3])` |           |       | 8    |

`**An`

| Declaration    | Compiles? | Null? | Size |
| -------------- | --------- | ----- | ---- |
| `int A1[3]`    | N         | -     | -    |
| `int *A2[3]`   | Y         | Y     | 4    |
| `int (*A3)[3]` |           |       | 4    |
| `int (*A4[3])` |           |       | 4    |

## Multidimensional (Nested) Arrays

`A[R][C]` is an array of `R` elements, where each element is an array of `C` sub-elements

> Think of that "nesting". When you read declarations, you start from the name of the element, and you work your way outward through these brackets and stars, in some order.
