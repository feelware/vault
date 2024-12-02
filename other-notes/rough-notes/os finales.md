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

#wip
- Learn what TLB is
- Learn how to compute TLB misses

###### 8.7

Of the following items, which are stored in the **thread control block**, which are stored in the **process control block**, and which in neither?

**Page table pointer**

**Page table**

**Stack pointer**

**Segment table**

**Ready list**

**CPU registers**

**Program counter**

#wip
- Learn the details of TCB and PCB
- Learn what each of the listed items means

###### 8.8

Draw the segment and page table for the 32-bit Intel architecture

notes
- no creo que venga

###### 8.9

Draw the segment and page table for the 64-bit Intel architecture

notes
- no creo que venga

###### 8.11

Suppose you are designing a system with paged segmentation, and you anticipate the memory **segment size** will be *uniformly* distributed between 0 and 4 GB. The overhead of the design is the **sum** of the **internal fragmentation** and the **space taken up by the page tables**. If each page table entry uses four bytes per page, what **page size** *minimizes* overhead?

In other words:

- Segment size: Uniformly distributed between 0 and 4 GB
- Overhead = Page tables + Fragmentation
- Page table = 4 bytes * Number of page entries
- Find page size that minimizes overhead

#wip 
- understand segmented memory (and segment tables)
- understand paged memory (and page tables)
- understand paged segmentation

###### 8.12

In an architecture with paged segmentation, the 32-bit virtual address is divided into fields as follows:

4 bit segment number - 12 bit page number - 16 bit offset

The segment and page tables are as follows (all values in hexadecimal):


| Segment Table   | Page Table A     | Page Table B     |
| --------------- | ---------------- | ---------------- |
| 0 Page Table A  | 0 CAFE           | 0 F000           |
| 1 Page Table B  | 1 DEAD           | 1 D8BF           |
| x (res invalid) | 2 BEEF           | 2 3333           |
|                 | 3 BA11           | x (rest invalid) |
|                 | x (rest invalid) |                  |

Find the physical address corresponding to each of the following virtual addresses (answer "invalid virtual address" if the virtual address is invalid):

**0000000044**

**20022002**

**10015555**

#wip 
- learn how to compute physical addresses from virtual addresses given page and segment configurations

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

###### 11.4

Consider a text editor that saves a file whenever you click a save button. Suppose that when you press the button, the editor simply (1) animates the button “down” event (e.g., by coloring the button grey), (2) uses the `write()` system call to write your text to your file, and then (3) animates the button “up” event (e.g., by coloring the button white). What bad thing could happen if a user edits a file, saves it, and then turns off her machine by flipping the power switch (rather than shutting the machine down cleanly)?

###### 11.5

Write a program that times how long it takes to issue 100,000 one-byte writes in each of two ways. Explain your results. 

1. First, time how long it takes to use the POSIX system calls `creat()`, `write()`, and `close()` directly.

3. Then see how long these writes take if the program uses the `stdio` library calls (e.g., `fopen()`, `fwrite()`, and `fclose()`) instead.

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
Platters/Heads: 2/4
Capacity: 320 GB

**Performance**
Spindle speed: 7200 RPM
Average seek time read/write: 10.5 ms / 12.0 ms
Maximum seek time: 19 ms
Track-to-track seek time: 1 ms
Transfer rate (surface to buffer): 54-128 MB/s
Transfer rate (buffer to host): 375 MB/s
Buffer memory: 16 MB

**Power**
Typical: 16.35 W
Idle: 11.68 W

###### 12.6

Suppose I have a disk such as the 320 GB SATA drive described in Figure 12.9 and I have a workload consisting of 10000 reads to 10000 sequential sectors on the outermost tracks of the disk. How long will these 10000 requests take (total) assuming the disk services requests in FIFO order?

Figure 12.9 shows some key parameters for a 320 GB SATA disk drive:

**Size**
Form factor: 2.5 inch
Capacity: 320 GB

**Performance**
Spindle speed: 5400 RPM
Average seek time: 12.0 ms
Maximum seek time: 21 ms
Track-to-track seek time: 2 ms
Transfer rate (surface to buffer): 850 Mbit/s (maximum)
Transfer rate (buffer to host): 3 Gbit/s
Buffer memory: 8 MB

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
