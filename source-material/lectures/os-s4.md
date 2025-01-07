---
tags:
  - "#lecture-notes"
src-date: 2024-09-04
src-author: 
src-link:
---
# Operating Systems - Session 4

## Multiple Processor Scheduling
### Symmetric & Asymmetric Multiprocessing (SMP y AMP)

#wip

### Processor affinity

![](utilities/attachments/Pasted%20image%2020241002150519.png)

- Cache es "reservada" a estado de procesos (valores de registros) guardados durante un context switch
- Un procesador acceda más rápido a su propia cache que a la memoria principal cada vez que se quiera restaurar el proceso (1 ns vs. 5-10 ms)
 - **soft affinity**: no se garantiza mantener un proceso en un mismo procesador
 - **hard affinity**: sí hay garantía
 - syscall `sched_setaffinity(pid_t pid, size_t cpusetsize, const cpu_set_t *mask)` implementa hard affinity, restringiendo un proceso a un solo conjunto de procesadores
 - #wip diferencias entre core, thread (contexto de hardware), procesador y socket

### Non-Uniform Memory Access (NUMA)

![](utilities/attachments/Pasted%20image%2020241002152515.png)

- La afinidad de procesador es un factor a considerar por el scheduler
- cuando hay una ready queue por procesador, se debe asegurar que cada ready queue tenga al menos un proceso
- la mayoría de OS modernos tienen una ready queue por procesador
- **push migration**: un proceso verifica la carga del resto de procesadores y, cuando encuentra desbalances, empuja procesos de manera acorde
- **pull migration**: procesadores libres jalan procesos de procesadores con alta carga
- scheduler de freebsd (ule) y el de linux implementan ambas técnicas (no son excluyentes)

### Procesadores Multicore

![](utilities/attachments/Pasted%20image%2020241002154207.png)

#wip 

## Real-Time scheduling

- Hay sistemas críticos que requieren mínima latencia
- **soft real-time**: minimizas la latencia
- **hard real-time**: hay límites estrictos respecto a cuando un proceso será scheduled

### latencias

- **interrupt latency**: #wip
- **dispatch latency**: #wip

## Scheduling en Linux

- #wip ?????????
- `sched`
