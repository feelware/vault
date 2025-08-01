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
# ICS: Course Overview

## `int` != integer. `float` != real

Overflows cause certain assumptions about numbers to not be met

## It's important to understand the assembly output of programs

More than just learning to write assembly "by hand"

## It's important to understand the memory system

### Memory Referencing Bug Example

```c
#include <stdio.h>

typedef struct {
  int a[2];
  double d;
} struct_t;

double fun(int i) {
  volatile struct_t s;
  s.d = 3.14;
  s.a[i] = 1073741824;
  return s.d;
}

int main() {
  printf("%f\n", fun(0)); // a[0]
  printf("%f\n", fun(1)); // a[1]
  printf("%f\n", fun(2)); // d
  printf("%f\n", fun(3)); // d
  printf("%f\n", fun(4)); // ?
  printf("%f\n", fun(5)); // ?
  printf("%f\n", fun(6)); // critical state
}
```

Output:

```
3.140000
3.140000
3.14000
2.000001
3.140000
3.140000
*** stack smashing detected ***: terminated
zsh: IOT instruction (core dumped)  ./a.out
```

- C/C++ doesn't do bounds checking on arrays. It won't complain, but they OS might complain.
- Memory referencing errors can be really hard to debug

## There's more to performance than asymptotic complexity

```c
// rows by row (4.3 ms)
void copyij(int src[2048], int dest[2048]) {
	int i, j;
	for (i = 0; i < 2048; i++)
		for (j = 0; j < 2048; j++)
			dst[i][j] = src[i][j];
}

// column by column (81.8 ms)
void copyji(int src[2048], int dest[2048]) {
	int i, j;
	for (j = 0; j < 2048; j++)
		for (i = 0; i < 2048; i++)
			dst[i][j] = src[i][j];
}
```

Copying a matrix row-by-row is faster than col-by-col. Why do things like this happen?

## Computers not only execute programs

But also do I/O and communicate over the network, which lead to other challenges:

- Concurrent operations by autonomous processes
- Coping with unreliable media
- Cross platform compatibility
- Complex performance issues
