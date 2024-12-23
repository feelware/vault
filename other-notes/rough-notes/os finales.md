# finales

## sistemas operativos

### notas

- [Operating Systems - Session 5](../../source-material/lectures/Operating%20Systems%20-%20Session%205.md) (COMPLETE)
- [Operating Systems - Session 6](../../source-material/lectures/Operating%20Systems%20-%20Session%206.md) (COMPLETE)
- [Operating Systems - Session 7](../../source-material/lectures/Operating%20Systems%20-%20Session%207.md) (INCOMPLETE)

### preguntas del libro

#### [Volume 3](../../source-material/textbooks/osppv3.pdf)

##### Chapter 8: Address Translation

###### 8.6

Consider the following piece of code which multiplies two matrices:

```c
float a[1024][1024], b[1024][1024], c[1024][1024];

multiply() {
	unsigned i, j, k;

	for (i = 0; i < 1024; i++)
		for (j = 0; j < 1024; j++)
			for (k = 0; k < 1024; k++)
				c[i][j] += a[i][k] * b[k][j];
}
```

Assume that the binary for executing this function fits in one page and that the stack also fits in one page. Assume that storing a floating point number takes 4 bytes of memory. If the page size is 4 KB, the TLB has 8 entries, and the TLB always keeps the most recently used pages, compute the number of TLB misses assuming the TLB is initially empty.

**Respuesta:**

Cada matriz contiene $1024  * 1024 = 2^{20}$ elementos, ocupando un total de $4 * 2^{20}$ bytes. Dado que cada página contiene $4 * 2^{10}$ bytes, cada matriz ocupa $2^{10}$ páginas.

Podemos crear un programa básico en C que simule el funcionamiento de una TLB y, así, compute la cantidad de *misses*.

El TLB es implementado como una cola: los elementos son insertados de izquierda a derecha. Si la cola está llena y se desea insertar un nuevo elemento, el elemento más antiguo es eliminado y el resto es movido un paso a la izquierda, dejando espacio al final de la cola para el nuevo elemento.

```c
#include <stdio.h>
#include <stdbool.h>

// matrix size (in floats)
#define N 1024

// page size (in floats)
#define P 1024

// TLB capacity (in entries)
#define TLB_CAPACITY 8

unsigned int tlb_size = 0;
unsigned int tlb_misses = 0;
unsigned int tlb[TLB_CAPACITY];

// float a[N][N], b[N][N], c[N][N];

void init_tlb() {
	for (unsigned int i = 0; i < TLB_CAPACITY; i++)
	tlb[i] = -1;
}

bool is_in_tlb(unsigned int page) {
	for (unsigned int i = 0; i < TLB_CAPACITY; i++)
		if (tlb[i] == page)
			return true;
	return false;
}

void remove_oldest_from_tlb() {
	for (unsigned int i = 0; i < tlb_size - 1; i++)
		tlb[i] = tlb[i + 1];
	tlb_size--;
}

void insert_into_tlb(unsigned int page) {
	if (tlb_size == TLB_CAPACITY)
		remove_oldest_from_tlb();
	tlb[tlb_size++] = page;
}

void multiply() {
	unsigned int i, j, k;
	init_tlb();
	
	for (i = 0; i < N; i++)
		for (j = 0; j < N; j++)
			for (k = 0; k < N; k++) {
				unsigned int c_i = (i * N + j);
				unsigned int a_i = (i * N + k);
				unsigned int b_i = (k * N + j);
				
				unsigned int c_page = (c_i / P);
				unsigned int a_page = (a_i / P) + N;
				unsigned int b_page = (b_i / P) + N * 2;
				
				bool c_in_tlb = is_in_tlb(c_page);
				bool a_in_tlb = is_in_tlb(a_page);
				bool b_in_tlb = is_in_tlb(b_page);
				
				if (!c_in_tlb) {
					tlb_misses++;
					insert_into_tlb(c_page);
				}
				
				if (!a_in_tlb) {
					tlb_misses++;
					insert_into_tlb(a_page);
				}
				
				if (!b_in_tlb) {
					tlb_misses++;
					insert_into_tlb(b_page);
				}
				
				printf("C: [%d, %d]: %d\t\tpage %d\t%s\n", i, j, c_i, c_page, c_in_tlb ? "(hit)" : "(miss)");
				printf("A: [%d, %d]: %d\t\tpage %d\t%s\n", i, k, a_i, a_page, a_in_tlb ? "(hit)" : "(miss)");
				printf("B: [%d, %d]: %d\t\tpage %d\t%s\n", k, j, b_i, b_page, b_in_tlb ? "(hit)" : "(miss)");
				
				// c[i][j] += a[i][k] * b[k][j];
			}
	printf("TLB misses: %d\n", tlb_misses);
}

int main() {
	multiply();
}
```

###### 8.7

Of the following items, which are stored in the **thread control block**, which are stored in the **process control block**, and which in neither?

**Page table pointer**


**Page table**
En ninguno, cada proceso tiene su propio page table (asumiendo un solo nivel de traducción), pero no se almacena en ninguno de los dos control blocks.

**Stack pointer**
En el TCB, pues cada thread debe tener rastro de la ubicación de su propio stack.

**Segment table**
En el PCB, pues cada proceso tiene asignado un conjunto de segmentos.

**Ready list**
En ninguno, pues esta lista toma control de **todos** los procesos en espera de ser ejecutados.

**CPU registers**
En el TCB, pues cada thread debe saber cuál fue su último estado en el procesador.

**Program counter**
En el TCB, pues cada thread debe saber en qué punto de su ejecución se quedó.

###### 8.8

Draw the segment and page table for the 32-bit Intel architecture

![](../../utilities/attachments/Pasted%20image%2020241204084801.png)

![](../../utilities/attachments/Pasted%20image%2020241204084811.png)

###### 8.9

Draw the segment and page table for the 64-bit Intel architecture

###### 8.11

Suppose you are designing a system with paged segmentation, and you anticipate the memory **segment size** will be *uniformly* distributed between 0 and 4 GB. The overhead of the design is the **sum** of the **internal fragmentation** and the **space taken up by the page tables**. If each page table entry uses four bytes per page, what **page size** *minimizes* overhead?

- Sea $x$ el tamaño de página
- Sea $S$ la variable aleatoria que representa el tamaño de segmento (en bytes), tal que $S = \text{U}(0, 2^{30})$
- Tamaño esperado de segmento (en bytes): $E(S) = \dfrac{0 + 2^{30}}{2} = 2^{29}$ 
- La fragmentación internal es directamente proporcional al tamaño de página, así que podemos representarla como $kx$. Por practicidad, asumimos que $k = \dfrac{1}{2}$
- El número esperado de páginas por segmento es $\dfrac{E(S)}{x}$, ocupando un total de $4\dfrac{E(S)}{x} = \dfrac{2^{31}}{x}$ bytes
- El overhead total se puede representar como $h(x) = (\dfrac{x}{2} + \dfrac{2^{31}}{x})$ bytes
- Minimizamos $h$
$$
\begin{align*}
h'(x) = \dfrac{1}{2}-\dfrac{2^{31}}{x^2} &= 0 \\
x^2 &= 2^{32} \\
x &= 2^{16}
\end{align*}
$$
- Encontramos que el tamaño óptimo de página es $2^{16}$ bytes, pues lleva al overhead a su valor mínimo: $h(2^{16}) = 2^{16}$ bytes

###### 8.12

In an architecture with paged segmentation, the 32-bit virtual address is divided into fields as follows:

4 bit segment number - 12 bit page number - 16 bit offset

The segment and page tables are as follows (all values in hexadecimal):

| Segment Table    | Page Table A     | Page Table B     |
| ---------------- | ---------------- | ---------------- |
| 0 Page Table A   | 0 CAFE           | 0 F000           |
| 1 Page Table B   | 1 DEAD           | 1 D8BF           |
| x (rest invalid) | 2 BEEF           | 2 3333           |
|                  | 3 BA11           | x (rest invalid) |
|                  | x (rest invalid) |                  |

Find the physical address corresponding to each of the following virtual addresses (answer "invalid virtual address" if the virtual address is invalid):

- **00000000**

**Segment: 0**
`SegmentTable[0]` apunta a Page Table A

**Page number: 000**
`PageTableA[000]` apunta a page frame cuya base es `CAFE`

**Offset: `0000`**
Dirección final: `CAFE0000`

- **20022002**

**Segment: `2`**
Número de segmento inválido.
Dirección virtual inválida

- **10015555**

**Segment: 1**
`SegmentTable[1]` apunta a Page Table B

**Page number: 001**
`PageTableB[001]` apunta a page frame cuya base es `D8BF`

**Offset: `5555`**
Dirección final: `D8BF5555`

##### Chapter 9: Caching and Virtual Memory

###### 9.2

Most modern computer systems choose a page size of 4 KB.

a. Give a set of reasons why doubling the page size might increase performance.

b. Give a set of reasons why doubling the page size might decrease performance.

###### 9.8

Suppose a program repeatedly scans linearly through a large array in virtual memory. In other words, if the array is four pages long, its page reference pattern is `ABCDABCDABCD...`

For each of the following page replacement algorithms, sketch a graph showing the **rate of progress** (instructions per unit time) of each program as a function of the **physical memory available to the program**, from 0 to N, where N is sufficient to hold the entire array.

###### 9.9

Consider a computer system running a general-purpose workload with demand paging. The system has two disks, one for demand paging and one for file system operations. Measured utilizations (in terms of time, not space) are given in Figure 9.23.

|                       |       |
| --------------------- | ----- |
| Processor utilization | 20.0% |
| Paging Disk           | 99.7% |
| File Disk             | 10.0% |
| Network               | 5.0%  |

For each of the following changes, say what its likely impact will be on processor utilization, and explain why. Is it likely to significantly increase, marginally increase, significantly decrease, marginally decrease, or have no effect on the processor utilization?

**(a) Get a faster CPU**

**(b) Get a faster paging disk**

**(c) Increase the degree of multiprogramming**

###### Case study: Memory-Mapped Files

See Page 86

#### [Volume 4](../../source-material/textbooks/osppv4.pdf)

##### Chapter 11: File Systems (Introduction and overview)

###### 11.3

Write a program that creates a new file, writes 100 KB to it, flushes the writes, and deletes it. Time how long each of these steps takes.

**Hint**: You may find the POSIX system calls `creat()`, `write()`, `fflush()`, `close()`, and `gettimeofday()` useful. See the manual pages for details on how to use these.

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/time.h>

#define SIZE (100 * 1024)
#define NAME "test"

// calculate time difference (microseconds)
long long timediff(struct timeval *start, struct timeval *end) {
  return (end->tv_sec - start->tv_sec) * 1000000LL + (end->tv_usec - start->tv_usec);
}

int main() {
  struct timeval start, end;
  char *buffer;
  int file;

  buffer = malloc(SIZE);

  for (int i = 0; i < SIZE; i++)
    buffer[i] = i % 256;

  // create file
  gettimeofday(&start, NULL);
  file = creat(NAME, 0666);
  gettimeofday(&end, NULL);
  long long create_time = timediff(&start, &end);

  // write to it
  gettimeofday(&start, NULL);
  ssize_t bytes_written = write(file, buffer, SIZE);
  gettimeofday(&end, NULL);
  long long write_time = timediff(&start, &end);

  if (bytes_written != SIZE) {
    close(file);
    unlink(NAME);
    exit(1);
  }

  // flush the writes
  gettimeofday(&start, NULL);
  fflush(NULL);
  gettimeofday(&end, NULL);
  long long flush_time = timediff(&start, &end);

  close(file);

  // delete file
  gettimeofday(&start, NULL);
  unlink(NAME);
  gettimeofday(&end, NULL);
  long long delete_time = timediff(&start, &end);

  printf("create file: %lld\n",      create_time);
  printf("write to it: %lld\n",      write_time);
  printf("flush the writes: %lld\n", flush_time);
  printf("delete file: %lld\n",      delete_time);
}
```

- Creación de archivo: $26 \mu s$
- Escritura: $36 \mu s$
- Flush: $4 \mu s$
- Eliminación de archivo: $25 \mu s$
###### 11.4

Consider a text editor that saves a file whenever you click a save button. Suppose that when you press the button, the editor simply (1) animates the button “down” event (e.g., by coloring the button grey), (2) uses the `write()` system call to write your text to your file, and then (3) animates the button “up” event (e.g., by coloring the button white). What bad thing could happen if a user edits a file, saves it, and then turns off her machine by flipping the power switch (rather than 
shutting the machine down cleanly)?

Según la man page de `write`, las llamadas a `write` no son necesariamente escritas a disco de manera inmediata.

>   A successful return from `write()` does not make any guarantee that data has been committed to disk. [...] The only way to be sure is to call `fsync(2)` after you are done writing all your data.

Si la pérdida de energía se da durante la llamada a `write` se corre el riesgo de corromper el archivo, incluso si existe una llamada posterior a `fsync`, pues esta nunca se llega a ejecutar.

El escenario más probable es que la pérdida de energía ocurra tras un retorno exitoso por parte de `write`, pero aun sin haberse guardado los cambios a disco. En este caso, los cambios se pierden.

###### 11.5

Write a program that times how long it takes to issue 100,000 one-byte writes in each of two ways. Explain your results. 

1. First, time how long it takes to use the POSIX system calls `creat()`, `write()`, and `close()` directly.

2. Then see how long these writes take if the program uses the `stdio` library calls (e.g., `fopen()`, `fwrite()`, and `fclose()`) instead.

**Usando llamadas de `POSIX`**

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/time.h>

// number of bytes to write
#define N 100000

#define NAME "posix"

// calculate time difference (microseconds)
long long timediff(struct timeval *start, struct timeval *end) {
  return (end->tv_sec - start->tv_sec) * 1000000LL + (end->tv_usec - start->tv_usec);
}

int main() {
  struct timeval start, end;
  char byte = 'a';

  gettimeofday(&start, NULL);
  
  int fd = creat(NAME, 0666);
  if (fd == -1) {
    exit(1);
  }

  for (int i = 0; i < N; i++) {
    if (write(fd, &byte, 1) != 1) {
      close(fd);
      unlink(NAME);
      exit(1);
    }
  }

  close(fd);

  gettimeofday(&end, NULL);
  
  printf("posix: %lld\n", timediff(&start, &end));
  unlink(NAME);
}
```

**Usando llamadas de `stdio`**

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/time.h>

// number of bytes to write
#define N 100000

#define NAME "stdio"

// calculate time difference (microseconds)
long long timediff(struct timeval *start, struct timeval *end) {
  return (end->tv_sec - start->tv_sec) * 1000000LL + (end->tv_usec - start->tv_usec);
}

int main() {
  struct timeval start, end;
  char byte = 'a';

  gettimeofday(&start, NULL);
  
  FILE *file = fopen(NAME, "w");
  if (!file) {
    exit(1);
  }

  for (int i = 0; i < N; i++) {
    if (fwrite(&byte, 1, 1, file) != 1) {
      fclose(file);
      unlink(NAME);
      exit(1);
    }
  }

  fclose(file);

  gettimeofday(&end, NULL);
  
  printf("stdio: %lld\n", timediff(&start, &end));
  unlink(NAME);
}
```

Tras varias ejecuciones, es notorio que la versión `stdio` es más rápida (alrededor de 2000 $\mu s$) que la versión `POSIX` (alrededor de 65000 $\mu s$). Si corremos ambos programas con `strace` notaremos que, mientras la versión `POSIX` realiza 100001 llamadas a `write`, la versión `stdio` realiza solo 26.

```
$ strace --summary-only ./11-5-posix
posix: 1380664
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 99.76    0.288292           2    100001           write
  0.10    0.000292         292         1           execve
  0.04    0.000107          13         8           mmap
  0.02    0.000054          54         1           creat
  0.02    0.000049          49         1           unlink
  0.01    0.000034          11         3           mprotect
  0.01    0.000023          23         1           munmap
  0.01    0.000022          11         2           openat
  0.01    0.000019           6         3           close
  0.01    0.000019           6         3           fstat
  0.01    0.000019           6         3           brk
  0.00    0.000014           7         2           pread64
  0.00    0.000010          10         1         1 access
  0.00    0.000008           8         1           read
  0.00    0.000007           7         1           arch_prctl
  0.00    0.000007           7         1           prlimit64
  0.00    0.000006           6         1           set_tid_address
  0.00    0.000006           6         1           set_robust_list
  0.00    0.000006           6         1           rseq
  0.00    0.000003           3         1           getrandom
------ ----------- ----------- --------- --------- ----------------
100.00    0.288997           2    100037         1 total
```

```
$ strace --summary-only ./11-5-stdio
stdio: 1396
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
  0.00    0.000000           0         1           read
  0.00    0.000000           0        26           write
  0.00    0.000000           0         3           close
  0.00    0.000000           0         4           fstat
  0.00    0.000000           0         8           mmap
  0.00    0.000000           0         3           mprotect
  0.00    0.000000           0         1           munmap
  0.00    0.000000           0         3           brk
  0.00    0.000000           0         2           pread64
  0.00    0.000000           0         1         1 access
  0.00    0.000000           0         1           execve
  0.00    0.000000           0         1           unlink
  0.00    0.000000           0         1           arch_prctl
  0.00    0.000000           0         1           set_tid_address
  0.00    0.000000           0         3           openat
  0.00    0.000000           0         1           set_robust_list
  0.00    0.000000           0         1           prlimit64
  0.00    0.000000           0         1           getrandom
  0.00    0.000000           0         1           rseq
------ ----------- ----------- --------- --------- ----------------
100.00    0.000000           0        63         1 total
```

Esto demuestra que `stdio` no realiza llamadas al sistema para cada escritura, sino que las guarda en cache para luego ejecutarlas en lotes.

##### Chapter 12: Storage Devices

###### 12.1

**Discussion.** Some high-end disks in the 1980s had multiple disk arm assemblies per disk enclosure in order to allow them to achieve higher performance. Today, high- performance server disks have a single arm assembly per disk enclosure. Why do you think disks so seldom have multiple disk arm assemblies today?

###### 12.3

A disk may have multiple surfaces, arms, and heads, but when you issue a read or write, only one head is active at a time. It seems like one could greatly increase disk bandwidth for large requests by reading or writing with all of the heads at the same time. Given the physical characteristics of disks, can you figure out why no one does this?

###### 12.4

For the disk described in Figure 12.3, consider a workload consisting of 500 read requests, each of a randomly chosen sector on disk, assuming that the disk head is on the outside track and that requests are serviced in P-CSCAN order from outside to inside. How long will servicing these requests take?

*Note: Answering this question will require making some estimates.*

Figure 12.3 shows some key parameters for a recent 2.5-inch disk drive for laptop computers (Toshiba MK3254GSY) manufactured in 2008:

**Size**
- Platters/Heads: 2/4
- Capacity: 320 GB

**Performance**
- Spindle speed: 7200 RPM
- Average seek time read/write: 10.5 ms / 12.0 ms
- Maximum seek time: 19 ms
- Track-to-track seek time: 1 ms
- Transfer rate (surface to buffer): 54-128 MB/s
- Transfer rate (buffer to host): 375 MB/s
- Buffer memory: 16 MB

**Power**
- Typical: 16.35 W
- Idle: 11.68 W

- Seek time: Dado que la distribución de sectores solicitados es aleatoria, es difícil aprovechar el dato sobre CSCAN, así que usamos el seek time promedio para lecturas (10.5 ms)
- Rotation time: Nuevamente, no tenemos información suficiente sobre la posición del sector deseado al momento de llegar a su track, así que tomamos como estimado el tiempo que le toma un disco de 7200 RPM dar media revolución.
$$
\text{Average rotation time} =
\dfrac{1}{2} \cdot
\dfrac{1 \text{min}}{7200} \cdot
\dfrac{60 \text{s}}{1\text{min}} \cdot
\dfrac{1000 \text{ms}}{1\text{s}} = 4.17 \text{ms}
$$
- Transfer time: Dado que los sectores están en tracks aleatorios, una buena estimación para la tasa surface to buffer es el promedio de sus dos extremos (91 MB/s). No hay que olvidar el tiempo buffer to host, el cuál está a una tasa fija de 375 MB/s.
$$
\text{Average transfer time}
= \dfrac{512 \text{bytes}}{375 \cdot 10^3\text{bytes/ms}}
+ \dfrac{512 \text{bytes}}{91 \cdot 10^3\text{bytes/ms}}
= 0.007 \text{ms}
$$

Para una sola request, tenemos
$$
\text{Tiempo por request} = 10.5\text{ms} + 4.17\text{ms} + 0.007\text{ms} = 14.677\text{ms} 
$$
En total
$$
\text{Tiempo total} = 500 \cdot 14.677\text{ms} = 7.338\text{s} 
$$
###### 12.6

Suppose I have a disk such as the 320 GB SATA drive described in Figure 12.9 and I have a workload consisting of 10000 reads to 10000 sequential sectors on the outermost tracks of the disk. How long will these 10000 requests take (total) assuming the disk services requests in FIFO order?

Figure 12.9 shows some key parameters for a 320 GB SATA disk drive:

**Size**
- Form factor: 2.5 inch
- Capacity: 320 GB

**Performance**
- Spindle speed: 5400 RPM
- Average seek time: 12.0 ms
- Maximum seek time: 21 ms
- Track-to-track seek time: 2 ms
- Transfer rate (surface to buffer): 850 Mbit/s (maximum)
- Transfer rate (buffer to host): 3 Gbit/s
- Buffer memory: 8 MB

###### 12.7

Suppose I have a disk such as the 320 GB SATA drive described in Figure 12.9 and I have a workload consisting of 10000 reads to sectors randomly scattered across the disk. How long will these 10000 requests take (total) assuming the disk services requests using the SCAN/Elevator algorithm.

###### 12.8

Suppose I have a disk such as the 320 GB SATA drive described in Figure 12.9 and I have a workload consisting of 10000 reads to sectors randomly scattered across a 100 MB file, where the 100 MB file is laid out sequentially on the disk. How long will these 10000 requests take (total) assuming the disk services requests using the SCAN/Elevator algorithm?

###### 12.9

Write a program that creates a 100 MB file on your local disk and then measures the time to do each of four things. Explain your results:
 
**Sequential overwrite.** Overwrite the file with 100 MB of new data by writing the file from beginning to end and then calling `fsync()` (or the equivalent on your platform).
 
**Random buffered overwrite.** Do the following 50,000 times: choose a 2 KB- aligned offset in the file uniformly at random, seek to that location in the file, and write 2 KB of data at that position. Then, once all 50,000 writes have been issued, call `fsync()` (or the equivalent on your platform).
 
**Random buffered overwrite.** Do the following 50,000 times: choose a 2 KB- aligned offset in the file uniformly at random, seek to that location in the file, write 2 KB of data at that position, and call `fsync()` (or the equivalent on your platform) after each individual write.
 
**Random read.** Do the following 50,000 times: choose a 2 KB-aligned offset in the file uniformly at random, seek to that location in the file, and read 2 KB of data at that position.

###### 12.10

Write a program that creates three files, each of 100 MB, and then measures the time to do each of three things. Explain your results:

**`fopen()/fwrite()`.** Open the first file using `fopen()` and issue 256,000 sequential four-byte writes using `fwrite()`.

**`open()/write()`.** Open the second file using `open()` and issue 256,000 sequential four-byte writes using `write()`.

**`mmap()/store`.** Map the third file into your program’s memory using `mmap()` and issue 256,000 sequential four-byte writes by iterating through memory and writing to each successive word of the mapped file.

##### Chapter 13: Files and Directories

###### 13.12

A web client and web server are running on the same uniprocessor computer. They have an open connection and are ready to send/receive web requests. List a possible sequence of user-mode/kernel-mode boundary crossings (counting one for each direction, and including interrupts) needed for the client to issue a simple web request, the server to receive the request and fetch the data from the file system, and for the server to send the data to the client.

Assume that there is a low priority background task running on the processor, the current directory is cached, but the requested file is not in the server cache or the file system cache. Also assume that both the request and the requested file data are small (e.g., they fit inside a single disk block). You may assume any of the file systems described in this chapter, provided you label which one you are assuming.

##### Chapter 14: Reliable Storage

###### 14.5

Go to an on-line site that sells hard disk drives, and find the largest capacity disk you can buy for less than $200. Now, track down the spec sheet for the disk and, given the disk’s specified bit error rate (or unrecoverable read rate), estimate the probability of encountering an error if you read every sector on the disk once.

###### 14.6

Suppose we define a RAID’s access cost as the number of disk accesses divided by the number of data blocks read or written. For each of following configurations and workloads, what is the access cost?

**a. Workload: a series of random 1-block writes.**
**Configuration: mirroring**

**b. Workload: a series of random 1-block writes. 
Configuration: distributed parity**

**c. Workload: a series of random 1-block reads.** 
**Configuration: mirroring**

**d. Workload: a series of random 1-block reads.** 
**Configuration: distributed parity** 

**e. Workload: a series of random 1-block reads.** 
**Configuration: distributed parity with group size G and one failed disk**

**f. Workload: a long sequential write.** 
**Configuration: mirroring**

**g. Workload: a long sequential write.** 
**Configuration: distributed parity with a group size of G**

###### 14.7

Suppose that an engineer who has not taken this class tries to create a disk array with dual-redundancy but instead of using an appropriate error correcting code such as Reed-Solomon, the engineer simply stores a copy of each parity block on two disks, as in Figure 14.13.

![](../../utilities/attachments/Pasted%20image%2020241202071903.png)

Give an example of how a two-disk failure can cause a stripe to lose data in such a system. Explain why data cannot be reconstructed in that case.

###### 14.9

Many RAID implementations allow on-line repair in which the system continues to operate after a disk failure, while a new empty disk is inserted to replace the failed disk, and while regenerating and copying data to the new disk.

Sketch a design for a 2-disk, mirrored RAID that allows the system to remain on-line during reconstruction, while still ensuring that when the data copying is done, the new disk is properly reconstructed (i.e., it is an exact copy of other disk.)

In particular, specify

**(1) What is done by a recovery thread**

**(2) What is done on a read during recovery**

**(3) What is done on a write during recovery.**

Also explain why your system will operate correctly even if a crash occurs in the middle of reconstruction.

###### 14.12

Suppose I have a disk such as the one described in Figure 14.14 and a workload consisting of a continuous stream of updates to random blocks of the disk.

Assume that the disk scheduler uses the SCAN/Elevator algorithm.

(a) What is the throughput in number of requests per second if the application issues one request at a time and waits until the block is safely stored on disk before issuing the next request?

(b) What is the throughput in number of requests per second if the application buffers 100 MB of writes, issues those 100 MB worth of writes to disk as a batch, and waits until those writes are safely on disk before issuing the next 100 MB batch of requests? Suppose that we must ensure that – even in the event of a crash – the `i`th update can be observed by a read after crash recovery only if all updates that preceded the `i`th update can be read after the crash. That is, we have a FIFO property for updates – the i+1’st update cannot “finish” until the `i`th update finishes.

b.1. Design an approach to get good performance for this workload.

b.2. Explain why your design ensures FIFO even if crashes occur.

b.3. Estimate your approach’s throughput in number of requests per second. (For comparison with the previous part of the problem, your solution should not require significantly more than 100 MB of main-memory buffer space.)

(c) Design an approach to get good performance for this workload. (Be sure to explain how writes, reads, and crash recovery work.)

(d) Explain why your design ensures FIFO even if crashes occur.

(e) Estimate your approach’s throughput in number of requests per second.

![](../../utilities/attachments/Pasted%20image%2020241202053958.png)

### diapositivas de clase

- [12_memory_management](../../source-material/lectures/12_memory_management.pdf)
	- Access time: registers vs memory
	- Caching (L1, L2, L3)
	- Memory protection (Base & Bound)
	- Program execution
	- Swapping
- [13_memory_management_cont](../../source-material/lectures/13_memory_management_cont.pdf)
	- Memory fragmentation
	- Memory segmentation
	- Memory paging
- [14_storage_manegement](../../source-material/lectures/14_storage_manegement.pdf)
	- Disk structure
	- Disk scheduling algorithms
	- Sector format: header, data, trailer
	- Error correcting code
	- Raw IO
	- Boot sector
	- Bad blocks
- [14_storage_managment_cont](../../source-material/lectures/14_storage_managment_cont.pdf)
	- Swap space
	- RAID: Disk mirroring, data striping
- [15_file_systems](../../source-material/lectures/15_file_systems.pdf)
	- Layers of abstraction
		- I/O control
		- Basic file system
		- File-organization module
		- Logical file system
	- File access methods
	- Boot control block
	- Volume control block
	- Mount table
	- other file system structures
