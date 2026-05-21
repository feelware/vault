---
status: to do
deadline: 2026-05-06
class: tesis
---
- [ ] refinar approach
- [ ] refinar search strings
- [ ] aplicar en search strings en repositorios (no filtros)
- [ ] aplicar filtros (criterios de exclusión)
- [ ] descargar cada resultado (bibtex)
- [ ] pasar a parsif.al para
	- [ ] aplicar criterios de exclusion
	- [ ] generar tablas
- [ ] refinar explicación 

---

Creo que podemos considerar el subtema del ruido dentro de la propia técnica 2 (dentro de su lista de tags).

---

Dejando eso de lado, necesito volver a elaborar mi estrategia de búsqueda del SOTA. 

Algo importante es que el SOTA “Es todo el conocimiento desarrollado para resolver el problema de estudio”. Su finalidad es:

- Ver qué se ha investigado y qué no.
- Conocer las técnicas más recientes y, entre ellas, identificar la técnica más adecuada, para lo que se puede mejorar, mejorar sustancialmente o innovar.
- Conocer el proceso para resolver el problema.

Los pocos resultados retornados por una búsqueda preliminar restringidas al problema central (dificultades del entrenamiento auditivo en educación musical) y al tipo de propuesta que mi estudio propone (videojuegos o plataformas gamificadas) demuestran lo desacoplados que están ambas variables en la literatura.

Las mecánicas del videojuego propuesto por este estudio dependen de ciertos componentes, como la generación automática de ejercicios y la evaluación automática de performance, cuya implementación no es trivial y requiere del uso de técnicas que originalmente se esperaba encontrar en la búsqueda del SOTA. Ya que ningún estudio previo implementa las mismas mecánicas que mi propuesta, la búsqueda del SOTA en dichas técnicas debe realizarse fuera del contexto de mi problema central, es decir, como búsquedas adicionales a la ya realizada y no restringidas al contexto del entrenamiento auditivo. Una búsqueda para cada técnica.

No obstante, hay que tener en cuenta el siguiente ejemplo planteado por el profesor:

Problema: Identificar perfiles asociado a un hecho delictivo.

Suponga que:

- No existen trabajos que usan la técnica SVM para el problema de estudio
- La técnica SVM si se puede aplicar, si se cuenta con abundante datos.

¿Es SVM parte del estado del arte? No, SVM es una técnica genérica. No hay trabajos de aplicación de SVM al problema de estudio.

Dado esto, es necesario que toda búsqueda del SOTA esté en función de un problema, quizá no el problema central, pero sí un problema intermedio cuya relación con la técnica sea más fácil de observar. Para esto podemos referir a nuestros problemas específicos, específicamente:

- ¿Cómo implementar un modelo generador de estructuras melódicas simbólicas para la generación automática de ejercicios de dictado y repentización melódica?
- ¿Cómo implementar un modelo de análisis de similitud de estructuras melódicas simbólicas para evaluar la precisión de interpretaciones y transcripciones musicales?

(Adicional a estos problemas específicos, se hará una búsqueda del SOTA en modelos de Automatic Machine Transcription.)

Para enriquecer los resultados de cada búsqueda, podemos extender el dominio del problema hacia aquellos donde se espera que sean más aplicados. En el caso del análisis de similitud melódica, un claro ejemplo es la identificación de plagio. Esta "extensión de dominio" debería verse reflejado en el search string de cada búsqueda. Cada search string debería ser de la siguiente forma:

```
(tags sobre técnica) AND (tags sobre problema)
```

Este es un ejemplo de search string para la técnica 2:

```
(
	(
		"melodic"
		OR "music"
		OR "symbolic music"
	)
	AND "similarity"
)
AND
(
	"music transcription"
	OR "performance assesment"
	OR "plagiarism detection"
	OR "query by humming"
	OR "music information retrieval"
)
```

Ambos grupos de tags (técnica y problema) conectan entren sí con ANDs, y los tags dentro de ellos se conectan con ORs, de tal modo que los resultados siempre relacionen las técnicas de interés con los subproblemas previstos (y subproblemas análogos), pero manteniendo libertad para elegir cualquier combinación de estas (symbolic music similarity + plagiarism detection, melodic similarity + query by humming, etc). Podría añadir más de estas variantes para aumentar la posibilidad de encontrar resultados.

El punto es que debo realizar estas tres búsquedas sobre las técnicas EN CONJUNTO con una búsqueda en función del problema central que relacione solo el problema y la propuesta (no las técnicas). En la fase de desarrollo mostraré una clustered stacked column chart con los resultados de la búsqueda por repositorio, por cada una de las 4 búsquedas y para resultados brutos y pos-selección. Pero esto lo veré al final. Por ahora, necesito que redactes la subsección de planificación (explicar la forma en la que haré el SOTA), incluyendo las tablas que consideres necesarias y los apartados para colocar los search strings. Recuerda que esta sección, como cualquier subsección de una tesis, debe realizarse en prosa, por párrafos y no con subtítulos. Hazlo en inglés para yo traducirlo luego al español.

---

> [!note]
> cada cluster corresponde a un repositorio distinto, cada cluster tendrá 4 columnas: una para cada búsqueda, y cada columna será una "pila" de 3 segmentos superpuestos: el menos opaco y más grande para las busquedas totales, una un poco más intensa para las busquedas tras aplicar criterios de exclusión, y la más intensa (y más pequeña) para los resultados tras aplicar los criterios de exclusión.
