# Exercises

##  Chapter 2

### 2.5

**Define three styles of switching from user-mode to kernel-mode.**

- Tras una interrupción externa (producida por dispositivos I/O), se guarda el estado del proceso actual y se ejecuta el handler correspondiente a dicha interrupción.
- Tras una excepción de hardware (normalmente producto de ejecutar una instrucción ilegal) se procede igual que con una interrupción: se guarda el estado del proceso y se ejecuta el handler correspondiente.
- Tras una llamada a una syscall, se ejecuta el *user stub*, el cual realiza el cambio de modo y provoca la ejecución del *kernel stub*. 

### 2.6

**Define four styles of switching from kernel-mode to user-mode.**

- Al restaurar un proceso interrumpido por una interrupción externa, una excepción de procesador o una syscall, se restaura el estado de dicho proceso (valores de registros) y se cambia el modo a "usuario".
- Al iniciar un nuevo proceso, se suele usar la misma funcionalidad que permite retornar tras una interrupción.
- Ceder el procesador a un proceso en espera de ser ejecutado también implica restaurar su estado y cambiar el modo a "usuario."
- Enviar una señal a un proceso (upcall). 

### 2.7

**Most hardware architectures provide an instruction to return from an interrupt, such as `iret`. This instruction switches the mode of operation from kernel-mode to user-mode.**

**a) Explain where in the operating system this instruction would be used.**

#wip

**b) Explain what happens if an application program executes this instruction.**

#wip

### 2.10

**Which of the following components is responsible for loading the initial value in the program counter for an application program before it starts running: the compiler, the linker, the kernel, or the boot ROM?**

Al iniciar un nuevo proceso, la **kernel** aloja un kernel stack y, en él, almacena los valores iniciales para ciertos registros, incluyendo el program counter. Tras ejecutar `popad` e `iret`, estos valores son cargados en los registros correspondientes y la ejecución inicia.

### 2.15

**Explain the steps that an operating system goes through when the CPU receives an interrupt.**

### Antes del handler

- Se deshabilitan interrupciones.
- Se crean copias temporales de las `eflags`, stack segment (`ss`), stack pointer (`esp`), code segment (`cs`) e instruction pointer (`eip`).
- Se cambia el valor del `ss` y `esp` para que apunten al interrupt stack.
- Se guardan las copias temporales antes mencionadas en el interrupt stack.
- Se cambia el valor del `cs` y `eip` para que apunten a la ubicación en memoria del handler correspondiente.

### Dentro del handler

- Se guardan los valores de registros generales en el interrupt stack.
- Ya habiendo preservado el estado del proceso interrumpido, el handler continua con el resto de sus actividades.

### Al restaurar el proceso interrumpido

- Se restauran los registros generales almacenados en el interrupt stack.
- Con `iret` se restauran el resto de registros (`cs`, `eip`, `eflags`, `ss` y `esp`) y se cambia el modo a "usuario".
- El proceso interrumpido continua su ejecución.

## Chapter 3

### 3.1

**Can UNIX fork return an error? Why or why not?**
**Note: You can answer this question by looking at the manual page for fork, but before you do that, think about what the fork system call does. If you were designing this call, would you need to allow fork to return an error?**

`fork` normalmente retorna:
- `0` en el proceso hijo
- el PID del proceso hijo, en el proceso padre

Cuando ocurre un error (ya sea por límites del sistema, carencia de memoria u otros motivos), el hijo **no** es creado y `fork` retorna solo en el proceso padre. En estos casos, el valor retornado es `-1`. Tener un valor de error bien definido permite a los programas identificar un fallo en la operación y actuar de forma acorde.

### 3.3

**What happens if we run the following program on UNIX?**

```c
main () {
	while (fork () >= 0);
}
```

El programa se replica de manera **infinita** (la condición del bucle será verdad siempre que `fork` no falle) y **exponencial** respecto al tiempo. Esto se conoce como una *fork bomb*.

### 3.8

**How many processes are created if the following program is run?**

```c
main (int argc, char ** argv) {
	forkthem(5) 
} 

void forkthem (int n) {
	if (n > 0) {
		fork();
		forkthem(n-1);
	}
}
```

Sea $n$ el argumento entero y positivo con el que se llama a `forkthem` en `main`, y $P$ el total de procesos creados. Cada llamada a `fork` duplica un proceso, lo que significa que cada nivel de la recursión tendrá el doble de procesos que la anterior.

Podemos definir a $P$ en función de $n$

$$
P(n) = 2^n
$$

Dado que, en este caso, $n$ es igual a $5$, un total de $32$ procesos serán creados.

### 3.9

**Consider the following program. How many different copies of the variable `x` are there? What are their values when their process finishes?**

```c
main ( int argc , char ** argv ) {
	int child = fork ();
	int x = 5;             // x(padre e hijo1) = 5

	if (child == 0) {
		x += 5;            // x(hijo1) = 5 + 5 = 10
	} else {
		child = fork ();   // x(hijo2) = 5
		x += 10;           // x(padre e hijo2) = 5 + 10 = 15
		if (child) {
			x += 5;        // x(padre) = 15 + 5 = 20
		}
	}
}
```

Tal y como indican los comentarios del bloque de código, existen tres copias de `x`, una para el padre, otra para el hijo 1,  y otra para el hijo 2, cuyos valores terminan siendo 20, 10 y 15, respectivamente, al terminar el programa.

### 3.11

**Implement a simple Linux shell in C capable of executing a sequence of programs that communicate through a pipe. For example, if the user types `ls | wc`, your program should fork off the two programs, which together will calculate the number of files in the directory. For this, you will need to use several of the Linux system calls described in this chapter: `fork`, `exec`, `open`, `close`, `pipe`, `dup2`, and `wait`. Note: You will to replace `stdin` and `stdout` in the child process with the pipe file descriptors; that is the role of `dup2`.**



## Chapter 4

### 4.4

Write a program that has two threads. The first thread a simple loop that continuously increments a counter and prints a period (“.”) whenever the value of that counter is divisible by 10,000,000. Make the second thread repeatedly wait for the user to input a line of text and then print “Thank you for your input.” On your system, does the first thread makes rapid progress? Does the second thread respond quickly?

### 4.5

 Write a program that uses threads to perform a parallel matrix multiply. To multiply two matrices, $C = A * B$, the result entry $C_{i,j}$ is computed by taking the dot product of the $i$th row of $A$ and the $j$th column of $B$: $C_{i,j} = \sum_{k=0}^{N-1} A_{i,k} B_{k,j}$. We can divide the work by creating one thread to compute each value (or each row) in $C$, and then executing those threads on different processors in parallel, as shown in Figure 4.19.

![](utilities/attachments/Pasted%20image%2020241007083801.png)

### 4.6

 Write a program that uses threads to perform a parallel merge sort.

### 4.10

For the `threadHello` program, what is the minimum and maximum by number of times that the main thread enters the `WAITING` state?

### 4.11

Using simple threads, write a program that creates several threads and that then determines whether the threads package on your system allocates a fixed size stack for each thread or whether each thread’s stack starts at some small size and dynamically grows as needed.
**Hints:** You will probably want to write a recursive procedure that you can use to consume a large amount of stack memory. You may also want to examine the addresses of variables allocated to different threads’ stacks. Finally, you may want to be able to determine how much memory has been allocated to your process; most operating systems have a command or utility that an show resource consumption by currently running processes (e.g., top in Linux, Activity Monitor in OSX, or Task Manager in Windows.)

## Chapter 5

### 5.2

Show that solution 3 to the Too Much Milk problem is safe — that it guarantees that at most one roommate buys milk.

### 5.3

Precisely describe the set of possible outputs that could occur when the program shown in Figure 5.5 is run.

### 5.4

Suppose that you mistakenly creates an automatic (local) variable $v$ in one thread $t1$ and pass a pointer to $v$ to another thread $t2$. Is it possible for a write by $t1$ to some variable other than $v$ will change the state of $v$ as observed by $t2$? If so, explain how this can happen and give an example. If not, explain why not.

### 5.5

Suppose that you mistakenly creates an automatic (local) variable $v$ in one thread $t1$ and pass a pointer to $v$ it to another thread $t2$. Is it possible for a write by $t2$ to $v$ will cause $t2$ to execute the wrong code? If so, explain how. If not, explain why not.

### 5.6

Assuming Mesa semantics for condition variables, our implementation of the blocking bounded queue in Figure 5.8 does not guarantee freedom from starvation: if a continuous stream of threads makes `insert()` (or `remove()`) calls, a waiting thread could wait forever. For example, a thread may call `insert` and wait in the `while` loop because the queue is full. Starvation would occur if every time another thread removes an item from the queue and signals the waiting thread, a *different* thread calls `insert`, sees that the queue is not full, and inserts an item before the waiting thread resumes.

Prove that under Hoare semantics and assuming that signal wakes the longest-waiting thread, our implementation of BBQ ensures freedom from starvation. More precisely, prove that if a thread waits in insert, then it is guaranteed to proceed after a bounded number of remove calls complete, and vice versa.

### 5.8

Wikipedia provides an implementation of Peterson's algorithm to provide mutual exclusion using loads and stores at http://en.wikipedia.org/wiki/Peterson’s_algorithm. Unfortunately, this code is not guaranteed to work with modern compilers or hardware. Update the code to include memory barriers where necessary. (Of course, you could add a memory barrier before and after each instruction; your solution should instead add memory barriers only where necessary for correctness.)

### 5.9

Linux provides a `sys_futex()` system call to assist in implementing hybrid user-level/kernel-level locks and condition variables.

A call to long `sys futex(void *addr1, FUTEX_WAIT, int val1, NULL, NULL, 0)` checks to see if the memory at address `addr1` has the same value as `val1`. If so, the calling thread is suspended. If not, the calling thread returns immediately with the error return value `EWOULDBLOCK`. In addition, the system call returns with the value `EINTR` if the thread receives a signal.

A call to `long sys_futex(void *addr1, FUTEX_WAKE, 1, NULL, NULL, 0)` causes one thread waiting on `addr1` to return.

Consider the following (too) simple implementation of a hybrid user- level/kernel-level lock.

```c++
class TooSimpleFutexLock {
	private:
		int val;
	
	public:
		TooSimpleMutex () : val (0) { } // Constructor
		
	void Acquire () {
		int c;
		while ((c = atomic_inc (val)) != 0){ // atomic_inc returns * old * value 
			futex_wait (& val , c + 1);
		}
	}
	
	void Release () {
		val = 0;
		futex_wake (&val, 1);
	}
};
```

There are three problems with this code.

- (a.) **Performance.** The goal of this code is to avoid making expensive system calls in the uncontested case when an acquire on a `FREE` lock or a release of a lock with no other waiting threads. This code fails to meet this goal. Why?

- (b.) **Performance.** A subtle corner case when multiple threads try to acquire the lock at the same time. It can show up as occasional slowdowns and bursts of CPU usage. What is the problem?

- (c.) **Correctness.** A corner case can cause the mutual exclusion correctness condition to be violated, allowing two threads to both believe they hold the lock. What is the problem?

### 5.13

For the solution to Too Much Milk suggested in the previous problem, each call to `drinkMilkAndBuylfNeeded()` is atomic and holds the lock from the start to the end even if one roommate goes to the store. This solution is analogous to the roommate padlocking the kitchen while going to the store, which seems a bit unrealistic. Implement a better solution to `drinkMilkAndBuylfNeeded()` using both locks and condition variables. Since a roommate now needs to release the lock to the kitchen while going to the store, you will no longer acquire the lock at the start of this function and release it at the end. Instead, this function will call two helper-functions, each of which acquires/releases the lock. For example:

```c
int Kitchen::drinkMilkAndBuylfNeeded() {
	int iShouldBuy = waitThenDrink();
	if (iShoudBuy) {
		buyMilk ();
	}
}
```

In this function, `waitThenDrink()` should wait if there is no milk (using a condition variable) until there is milk, drink the milk, and if the milk is now gone, return a nonzero value to flag that the caller should buy milk. `BuyMilk()` should buy milk and then broadcast to let the waiting threads know that they can proceed.

Again, test your code with varying numbers of threads.

## Chapter 6

## 6.1

Figure 6.13 shows the parallel execution of some requests in parallel and an equivalent sequential execution —request 1 then request 2 then request 3—. Two other sequential executions are also equivalent to the parallel execution shown in the figure. What are these other equivalent sequential executions?

![](utilities/attachments/Pasted%20image%2020241007090739.png)

### 6.2

Generalize the rules for two-phase locking to include both mutual exclusion locks and readers/writers locks. What can be done in the expanding phase? What can be done in the contracting phase?

## Chapter 7

### 7.2

Devise a workload where FIFO is pessimal —it does the worst possible choices— for average response time.

### 7.5

Is it possible for an application to run slower when assigned 10 processors than when assigned 8? Why or why not?

### 7.6

Suppose your company is considering using one of two candidate scheduling algorithms. One is Round Robin, with an overhead of 1% of the processing power of the system. The second is a wizzy new system that predicts the future and so it can closely approximate SJF, but it takes an overhead of 10% of the processing power of the system. Assume randomized arrivals and random task lengths. Under what conditions will the simpler algorithm outperform the more complex, and vice versa?

### 7.9

Is it possible for a system in equilibrium to have both bounded average response time and 100% utilization? Why or why not?

### 7.10

For a queueing system with random arrivals and service times, how does the variance in the service time affect the system response time? Briefly explain.

### 7.13

Three tasks, A, B, and C are run concurrently on a computer system.

- Task A arrives first at time 0, and uses the CPU for 100 ms before finishing.
- Task B arrives shortly after A, still at time 0. Task B loops ten times; for each iteration of the loop, B uses the CPU for 2 ms and then it does I/O for 8 ms.
- Task C is identical to B, but arrives shortly after B, still at time 0.

Assuming there is no overhead to doing a context switch, identify when A, B and C will finish for each of the following CPU scheduling disciplines:

a) FIFO
b) Round robin with a 1 ms time slice
c) Round robin with a 100 ms time slice
d) Multilevel feedback with four levels, and a time slice for the highest priority level is 1 ms.
e) Shortest job first

### 7.15

Explain how you would set up a valid experimental comparison between two scheduling policies, one of which can starve some jobs.

### 7.16

As system administrator of a popular social networking website, you notice that usage peaks during working hours (10 AM — 5 PM) and the evening (7 — 10 PM) on the US east coast. The CEO asks you to design a system where during these peak hours there will be three levels of users. Users in level 1 are the center of the social network, and so they are to enjoy better response time than users in level 2, who in turn will enjoy better response time than users in level 3. You are to design such a system so that all users will still get some progress, but with the indicated preferences in place.

a) Will a fixed priority scheme with pre-emption and three fixed priorities work? Why, or why not? 
b) Will a UNIX-style multi-feedback queue work? Why, or why not?

### 7.17

Consider the following preemptive priority-scheduling algorithm based on dynamically changing priorities. Larger numbers imply higher priority. Tasks are preempted whenever there is a higher priority task. When a task is waiting for CPU (in the ready queue, but not running), its priority changes at a rate of $a$:

$$
P(t) = P_0 + a \times (t - t_0)
$$

where $t_0$ is the time at which the task joins the ready queue and $P_0$ is its initial priority, assigned when the task enters the ready queue or is preempted. Similarly, when it is running, the task’s priority changes at a rate $b$, The parameters $a$, $b$ and $P_0$ can be used to obtain many different scheduling algorithms.

a) What is the algorithm that results from $P_0 = 0$ and $b > a > 0$?
b) What is the algorithm that results from $P_0 = 0$ and $a < b < 0$?
c) Suppose tasks are assigned a priority 0 when they arrive, but they retain their priority when they are preempted. What happens if two tasks arrive at nearly the same time and $a > 0 > b$?
d) How should we adjust the algorithm to eliminate this pathology?

### 7.20

A countermeasure is a strategy by which a user (or an application) exploits the characteristics of the processor scheduling policy to get as much of the processing time as possible. For example, if the scheduler trusts users to give accurate estimates of how long each task will take, it can give higher priority to short tasks. However, a countermeasure would be for the user to tell the system that the user’s tasks are short even when they are not.

Devise a countermeasure strategy for each of the following processor scheduling policies; your strategy should minimize an individual application’s response time (even if it hurts overall system performance). You may assume perfect knowledge —for example, your strategy can be based on which jobs will arrive in the future, where your application is in the queue, and how long the tasks ahead of you will run before blocking. Your strategy should also be robust— it should work properly even if there are no other tasks in the system, there are only short tasks, or there are only long running tasks. If no strategy will improve your application’s response time, then explain why.

a) Last in first out
b) Round robin, assuming tasks are put at the end of the ready list when they become ready to run
c) Multilevel feedback queues, where tasks are put on the highest priority queue when they become ready to run

### 7.21

Consider a computer system running a general-purpose workload. Measured utilizations (in terms of time, not space) are given in Figure 7.24.

For each of the following changes, say what its likely impact will be on processor utilization, and explain why. Is it likely to significantly increase, marginally increase, significantly decrease, marginally decrease, or have no effect on the processor utilization?

![](utilities/attachments/Pasted%20image%2020241007092440.png)

a) Get a faster CPU
b) Get a faster disk
c) Increase the degree of multiprogramming
d) Get a faster network

### Case Study: Servers in a Data Center

We can illustrate the application of the ideas discussed in this chapter, by considering how we should manage a collection of servers in a data center to provide responsive web service. Many web services, such as Google, Facebook, and Amazon, are organized as a set of front-end machines that redirect incoming requests to a larger set of back-end machines. We illustrate this in Figure 7.23.

![](utilities/attachments/Pasted%20image%2020241007093436.png)

This architecture isolates clients from the architecture of the back-end systems, so that more capacity can be added to the back-end simply by changing the configuration of the front-end systems. Back-end servers can also be taken off-line, have their software upgraded, and so forth, completely transparently to clients.

To provide good response time to the clients of the web service:

- When clients first connect to the service, the front-end node assigns each customer to a back-end server to balance load. Customers can be spread evenly across the back-end servers or they can be assigned to a node with low current load, much as customers at a supermarket select the shortest line for a cashier.
- Additional requests from the same client can be assigned to the same back-end server, as a form of affinity scheduling. Once a server has fetched client data, it will be faster for it to handle additional requests.
- We need to prevent individual users from hogging resources, because that can disrupt performance for other users. A back-end server can favor short tasks over long ones; they can also keep track of the total resources used by each client, reducing the scheduling priority of any client consuming more than their fair share of resources.
- It is often crucial to the usability of a web service to keep response time small. This requires monitoring both the rate of arrivals and the average amount of computing, disk, and network resources consumed by each request. Back-end servers should be added before average server utilization gets too high.
- Since it often takes considerable time to bring new servers online, we need to predict future load and have a backup plan for overload conditions.
