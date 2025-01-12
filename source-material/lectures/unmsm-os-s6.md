---
tags:
  - "#lecture-notes"
src-date: 2024-09-04
src-author:
  - Edson Ticona
src-link:
---
# Operating Systems - Session 6

## Dynamic storage allocation problem

- First fit: El primer hueco lo suficientemente grande
- Best fit: El hueco más pequeño suficientemente grande
- Worst fit: El hueco más grande
- First fit y best fit son los mejores en la práctica, con resultados similares

## Fragmentación

- Huecos pequeños dispersos a lo largo de la memoria
- Los tres tipos mencionados antes sufren fragmentación
- First fit: En promedio se pierden $0.5n$ bloques de memoria al alojar $n$ bloques
- Una solución es re-arreglar la memoria para que todos los procesos estén de un lado, dejando un hueco grande del otro lado. Esta solución no suele valer la pena en la práctica.

## Segmentación

#wip

![Pasted image 20241113154521](../../utilities/attachments/Pasted%20image%2020241113154521.png)

## Paginado

![Pasted image 20241113162155](../../utilities/attachments/Pasted%20image%2020241113162155.png)
- Tanto direcciones lógicas como físicas tienen dos componentes.
- #wip
![Pasted image 20241113162216](../../utilities/attachments/Pasted%20image%2020241113162216.png)
- Nota: Memoria lógica y memoria virtual son diferentes
