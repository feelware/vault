# Hoy en Sergio

## Granollers

- usar Claude para introducir al método de Granollers y explicar como se hizo la evaluación usando como base la fuente de Granollers
* usar el articulo de Granollers para obtener las preguntas del cuestionario y la idea de usar 4 posibles respuestas (not applicable, no, neither, yes) (1 fuente)
* mencionar que este artículo no esclarece como calcular el porcentaje de usabilidad, por lo que nosotros proponemos un simple promedio.
- sean $n$, $e$ y $s$ las cantidad de respuestas contestadas con no, neither y yes respectivamente para cierta pregunta, calculamos así el score $x$ de dicha pregunta:

$$
x = \dfrac{s + 0.5e}{s + e + n}
$$

- calculamos así el porcentaje de usabilidad $U$ como el promedio de los scores de todas las preguntas

$$
U = \overline{x} \cdot 100\%
$$

**Prompt:**

Ahora toca redactar la parte de Pruebas y Validación, el cuál se dividirá en dos partes.

1. Evaluación del editor 2D usando el método de Granollers
2. Evaluación de la visualización 3D usando telemetría enviada desde el navegador al servidor.

Por ahora enfoquémonos en la primera parte. Se tomará como base un paper llamado "Automation of Granollers Heuristic Evaluation Method Using a Developed Support System: A Case Study". Este paper propone una forma de automatizar el método de Granollers en comparación con la manera tradicional de hacerlo. Esto no nos interesa ahora, solo nos interesa la manera tradicional. En nuestro caso, se contactó a cinco evaluadores a través de una comunidad online de UX, quienes contestaron un formulario de Google Forms con todas las preguntas del método de Granollers, esto después de haber probado la plataforma y el editor 2D. El paper de referencia solo se usará para explicar el background teórico del método de Granollers, para saber qué preguntas colocar en el formulario y las posibles respuestas a cada pregunta (Yes, Neither, No, Not applicable) así como los puntajes asociados a cada una de estas respuestas (1, 0.5, 0, no considerado al promediar).

Tengo planeado esta estructura:

- Explicación breve del método de evaluación heurística de Granollers.
- Método: Reclutamiento de evaluadores, en esta parte tambien mostraré las preguntas del formulario, no tienes que escribir esta lista tú, solo coloca la etiqueta [TABLA] para saber en donde tengo que pegar yo la tabla con todas las preguntas. 
- Análisis de resultados: Algo que tambien debe mencionarse es que el estudio de referencia no es transparente respecto a cómo computa el coeficiente de usabilidad a partir de las respuestas al formulario, por lo que nosotros proponemos el siguiente método:
	- sean $n$, $e$ y $s$ las cantidad de respuestas contestadas con no, neither y yes respectivamente para cierta pregunta, calculamos así la puntuación $x$ de dicha pregunta:
$$
x = \dfrac{s + 0.5e}{s + e + n}
$$
	- calculamos la puntuación $H$ para cierta heurística como el puntaje promedio para todas las preguntas de dicha heurística
$$
H = \overline{x_p}
$$
	- similarmente, calculamos el porcentaje de usabilidad $U$ como el puntaje promedio para todas las preguntas realizadas
$$
U = \overline{x}
$$
- Explicar cómo saber qué heurísticas tienen menor puntuación nos ayuda a identificar áreas de mejora para el editor.

## OGAR

- usar los artículos de Paolo sobre OGAR para slopear con Claude unos párrafos sobre evaluación de galerías 3d (2 fuentes)
- falsificar plots de usuarios interactuando con galeria
