# Sistemas operativos: Examen final

Estudiante: **Jesus Stevan Diaz Ingol**

## Pregunta 1

- a. Verdad. Los SSDs, a diferencia de los HDDs, son de acceso aleatorio, haciendo innecesario optimizar el tiempo de acceso a través de algoritmos de I/O scheduling. 
- b. Verdad. Los procesadores cuentan con un memory management unit (MMU) que traduce direcciones virtual a direcciones físicas.
- c. Verdad. La memoria caché suele ser gestionada por el hardware, más que el sistema operativo.
- d. 

## Pregunta 2

Las lecturas/escrituras usuales requieren que los procesos realicen llamadas al sistema, pues estos no tienen los privilegios necesario para interactuar con archivos directamente. Mapear archivos en memoria elimina "el hombre del medio", haciendo que estos sean visibles para los procesos de usuario, lo cual es más rápido. Esto también permite que varios procesos trabajen sobre los mismos archivos en simultáneo.

## Pregunta 3

Usar tamaños de página muy grandes puede conllevar a fragmentación interna, es decir, que buen porcentaje de estas páginas se quede sin utilizar. Por otro lado, usar tamaños de página muy pequeños extiende el tamaño de las *page tables*. Ambos extremos pueden generar desperdicio de memoria, por lo que es necesario encontrar un buen punto medio, el cual suele ser 4 KB.

## Pregunta 4

Asumimos las siguientes especificaciones para el disco hipotético:

- Seek time promedio (lectura): 10 ms
- Seek time máximo: 20 ms
- Velocidad de spindle: 10000 RPM
- Tasa de transferencia (surface to buffer): 50-150 MB/s
- Tasa de transferencia (buffer to host): 500 MB/s

### FIFO

Usamos la siguiente fórmula para calcular el tiempo total:

$$
\text{Total time} = N (\text{Seek time} + \text{Rotation time} + \text{Transfer time})
$$

#### Seek time

Dado que la distribución de sectores solicitados es aleatoria, usamos el seek time promedio para lecturas (10 ms).

#### Rotation time

No tenemos información suficiente sobre la posición del sector iniciar al momento en que la cabeza llega al track indicado, así que tomamos como aproximación el tiempo que le toma un disco de 10000 RPM dar media revolución.

$$
\text{Rotation time} =
\dfrac{1}{2} \cdot
\dfrac{1 \text{min}}{10000} \cdot
\dfrac{60 \text{s}}{1\text{min}} \cdot
\dfrac{1000 \text{ms}}{1\text{s}} = 3 \text{ms}
$$

#### Transfer time

Dado que los sectores están en tracks aleatorios, una buena estimación para la tasa surface to buffer es el promedio de sus dos extremos (100 MB/s). No hay que olvidar la transferencia buffer to host, el cuál está a una tasa fija de 500 MB/s.

$$
\text{Transfer time}
= \dfrac{512 \text{bytes}}{100 \cdot 10^3\text{bytes/ms}}
+ \dfrac{512 \text{bytes}}{500 \cdot 10^3\text{bytes/ms}}
= 0.006 \text{ms}
$$


En total, tenemos
$$
\text{Total time} = 1000 (10\text{ms} + 3\text{ms} + 0.006\text{ms}) = 13.006\text{s} 
$$

### CSCAN

Esta vez la fórmula cambia. A diferencia de FIFO, el brazo ya no debe moverse tanto en cada request. Basta en girar un aproximado de dos recorridos enteros: uno en una dirección para atender a todas las requests, y otro en la dirección contraria para regresar a donde empezó.

$$
\text{Total time} = 2 \cdot \text{Maximum seek time} + N (\text{Rotation time} + \text{Transfer time})
$$

Reusamos los valores ya obtenidos:

$$
\text{Total time} = 2 \cdot 20\text{ms} + 1000(3\text{ms} + 0.006\text{ms}) = 3.046\text{s}
$$

Notamos que CSCAN resulta en un tiempo $9.96\text{s}$ menor que FIFO debido a su manejo inteligente del brazo del disco.

## Pregunta 5

```c
#include <stdio.h>
#include <unistd.h>
#include <semaphore.h>
#include <sys/stat.h>

struct inode {
  unsigned int mode;
  uid_t uid;
  gid_t gid;
  sem_t sem;
};

int _symlink(struct inode* file, const char* target_path, const char* link_path) {
  if (sem_wait(&file->sem) == -1)
    return -1;

  int result = symlink(target_path, link_path);

  if (result == -1) {
    sem_post(&file->sem);
    return -1;
  }

  chmod(link_path, file->mode);
  chown(link_path, file->uid, file->gid);

  sem_post(&file->sem);

  return result;
}

int _mkdir(struct inode* dir, const char* path, mode_t mode) {
  if (sem_wait(&dir->sem) == -1) return -1;

  int result = mkdir(path, mode);
  
  if (result == -1) {
    sem_post(&dir->sem);
    return -1;
  }

  chown(path, dir->uid, dir->gid);
  
  sem_post(&dir->sem);

  return result;
}

int main() {
  struct inode file_info = {
    .uid = getuid(),
    .gid = getgid(),
  };

  sem_init(&file_info.sem, 0, 1);

  int symlink_result = _symlink(&file_info, "target", "linkpath");
  int mkdir_result = _mkdir(&file_info, "dir", 0755);

  sem_destroy(&file_info.sem);

  return 0;
}

```

## Pregunta 6

TempleOS
