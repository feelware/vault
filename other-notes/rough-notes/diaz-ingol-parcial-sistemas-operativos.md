# Examen Parcial - Sistemas Operativos

**Alumno**: Jesus Stevan Diaz Ingol

**Código de estudiante**: 22200083

## 1. Veracidad o falsedad

> Un scheduler corriendo sobre un procesador de un único núcleo está libre de deadlocks o starvation pues existe un único thread de hardware.

Una deadlock ocurre cuando múltiples procesos dependen cíclicamente entre sí para continuar con su ejecución. Estos procesos pueden correr en el mismo procesador. Por otro lado, la starvation ocurre cuando procesos de baja prioridad nunca son atendidos. Ninguna de estas situaciones es afectada por la presencia de multiples procesadores, por lo tanto, la afirmación es falsa.

> Las únicas maneras de ir del espacio de kernel al espacio de usuario es llamando a una syscall o a través de una interrupción, sea de timer o de hardware.

La afirmación es incorrecta porque tanto las interrupciones como las syscalls son maneras de pasar del espacio de usuario al espacio de kernel, no al revés, como menciona la afirmación.

> La única manera de compartir data entre procesos concurrentes es a través del uso adecuado de primitivas de sincronización.

No son la única manera. Distintos procesos pueden comunicarse entre sí a través de, por ejemplo, upcalls, por lo que la afirmación es falsa.

## 2. Matemáticos

Este problema es un clásico ejemplo de deadlocks. Un lineamiento general para prevenir esta clase de problemas es asignar un orden global sobre los recursos a compartir y hacer que quienes los adquieran lo hagan en el orden establecido.

En este caso, se debe asignar un índice único a cada palillo. Ahora, cada matemático debe seguir el siguiente algoritmo cada vez que desee comer:

1. De los dos palillos a su disposición, intentar obtener el de menor índice
2. Intentar obtener el otro palillo a su disposición
3. Comer
4. Soltar ambos palillos

A modo de ejemplo, consideremos solo tres matemáticos $A$, $B$ y $C$, y tres palillos con índices 1, 2 y 3, tal y como se muestra en las figuras 1 al 6.

![Tres matemáticos y tres palillos. Cualquier matemático puede empezar a comer primero](utilities/attachments/Pasted%20image%2020241009152605.png)

![Supongamos que B decide comer primero. B adquiere 1, su palillo menor](utilities/attachments/Pasted%20image%2020241009152721.png)

![Para empezar a comer, B debe adquirir su palillo mayor: 2. A adquiere 2, su palillo menor, antes que B lo adquiera. B debe esperar](utilities/attachments/Pasted%20image%2020241009152828.png)

![A adquiere 3, su palillo mayor, siendo ahora capaz de comer. B sigue esperando a que A termine de comer. Poco después, C decide comer e intenta adquirir 1, su palillo menor, el cual está ocupado por B](utilities/attachments/Pasted%20image%2020241009152953.png)

![A termina de comer y libera sus palillos. B ahora puede adquirir 2 y comer. C sigue esperando a que B libere 1](utilities/attachments/Pasted%20image%2020241009153130.png)

![B termina de comer y libera sus palillos, lo que permite a C adquirir 1. C adquiere 3 y come.](utilities/attachments/Pasted%20image%2020241009153238.png)

## 3. Shell

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/types.h>
#include <sys/wait.h>

int process_line(char *line) {
	char *cmd;
	int pipes = 0;

	// contar pipes
	for (int i = 0; i < strlen(line); i++) {
		if (line[i] == '|') {
			pipes++;
		}
	}

	// crear pipes
	int fd[2 * pipes];
	for (int i = 0; i < pipes; i++) {
		if (pipe(fd + i * 2) == -1) {
			return 1;
		}
	}

	int cmd_i = 0;

	while (cmd = strtok_r(line, "|", &line)) {
		const char* file;
		char *token;

		// contar argumentos
		char *cmd_copy = strdup(cmd);
		int argc = 0;
		while (token = strtok_r(cmd_copy, " ", &cmd_copy)) {
			if (argc == 0) {
				file = token;
			}
			argc++;
		}

		// preparar lista de argumentos
		char *argv[argc + 1];
		for (int i = 0; i < argc; i++) {
			argv[i] = strtok_r(cmd, " ", &cmd);
		}
		argv[argc] = NULL;

		int child = fork();
		if (child == 0) {
			if (pipes > 0) {
				if (cmd_i == 0) {
					// primer comando solo escribe
					dup2(fd[1], 1);
				}
				else if (cmd_i == pipes) {
					// último comand solo lee
					dup2(fd[2 * (pipes - 1)], 0);
				}
				else {
					// comandos intermedios leen y escriben
					dup2(fd[2 * (cmd_i - 1)], 0);
					dup2(fd[2 * cmd_i + 1], 1);
				}
			}
			execvp(file, argv);
		}
		else {
			wait(child);
			cmd_i++;
		}
	}
	return 0;
}


int main(int argc, char *argv[]) {
	char *line;

	while (1) {
		printf("$ ");
		scanf("%99[^\n]", line);
		getchar();
		process_line(line);
	}
	
	return 0;
}
```

## 5. Debugging

El problema principal reside en la asignación `x = temp` fuera de la sección crítica. Esto da a pie a la posibilidad que ciertas actualizaciones sobre `x` hechas por un hilo sean sobreescritas por otro hilo, haciendo el valor de `x` inconsistente entre distintas ejecuciones. Esto se puede arreglar con tan solo mover dicha asignación dentro de la sección crítica.

```c
for (int i = 0; i < TASKS_PER_WORKER; i++) {
	pthread_mutex_lock(&lock);
	
	int temp = x;
	temp++;
	usleep(1);
	x = temp;        // después
	
	pthread_mutex_unlock(&lock);

	// x = temp;     // antes
}
```