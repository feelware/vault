---
tags:
  - "#lecture-notes"
src-date: 2024-09-04
src-author: 
src-link:
---
# Operating Systems - Session 5

- Ciclo de ejecución de instrucción
	- Fetch, decode, execute
	- Ocurre en un solo ciclo de reloj (generalmente)
- Las instrucciones deben estar cargadas en memoria (no en disco).
- Acceder y operar con registros suele tomar un ciclo de reloj, en ocasiones unos cuantos más.
- Acceder a memoria principal puede tomar varios ciclos. Las caches (L1, L2, L3) resuelven esto.
- La memoria caché suele ser gestionada por hardware
- Registros `base` y `limit` determinan los "bordes" del bloque de memoria de un proceso.
![](utilities/attachments/Pasted%20image%2020241106144616.png)
- Hardware realiza esta verificación de direcciones
- En tablas `GDT` y `LDT` se guardan los valores de los registros de segmentación

## Address binding

#wip

## Ejecución de un programa

 - **Static linking**: Librería ya compilada es adjuntada al binario de tu ejecutable (no dependencias)
 - **Dynamic linking**: Librería es carga de forma independiente por el sistema operativo y es usado por muchos procesos en simultáneo #wip 
- Primeros bytes de un ejecutable determinan el formato ("magic numbers")
- Dentro del ejecutable, existe una tabla con los símbolos usados por el programa y la ubicación de las librerías que las contienen (tabla de símbolos) #wip
- No todo el ejecutable se carga en memoria
- Una sección del ejecutable contiene data estática (`data`)
- Una sección del ejecutable contiene las instrucciones de CPU (`text`)
- `strings`: imprime los strings de un ejecutable
- `sha256sum`: calcular el sha256 de un ejecutable
- `file`: determina el tipo de archivo

## Swapping

#wip

![](utilities/attachments/Pasted%20image%2020241106162844.png)

- **input queue**: procesos que están esperando a ser cargados en memoria
- swapping: guardar proceso en disco cuando la RAM se llena
- **ready queue**: procesos guardados en disco (swapped)
- La mayoría de sistemas operativos no requieren crear una partición SWAP.
- `brk`: #wip
- `strace`: executes program and traces the system calls and signals