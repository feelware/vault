---
status: to do
deadline: 2025-10-08T18:00:00
class: inv
---
Terminar introducción

- Descartar párrafo 5 (situación problemática solo debe describir problema)

---

## Situación problemática

Párrafo 1:
- Definición fundamental de la síntesis de audio
- La síntesis de audio como elemento nuclear de la música electrónica, y cada vez más importante en la música contemporánea en general

Párrafo 2 (reconsiderar):
- Los primeros sintetizadores existieron en forma de hardware dedicado. La interfaz de estos sintetizadores solía incorporar un teclado similar al de un piano, cada tecla estando enlazada a una frecuencia de oscilación distinta y, por ende, una nota musical distinta.
- En la actualidad, los sintetizadores de software (*soft-synths*) implementan el estándar MIDI para permitir un control similar al de sus antecesores de hardware. Un dispositivo periférico llamado "controlador" cuenta con un teclado que no genera sonido por sí mismo: todo lo que hace es enviar un "evento" al computador cada vez que se presiona una tecla. Estos eventos describen qué notas musicales fueron tocadas y con qué intensidad, entre otros atributos. Finalmente, el sintetizador recibe estos eventos y emite las notas correspondientes.

Párrafo 3:
- Síntesis granular como técnica emergente (justificado por información sobre mercado de software de audio, posibles estadísticas de usuarios y casos de éxito notables, como su uso confirmado en algún soundtrack popular)
- Explicación fundamental de su funcionamiento: dividir una fuente de audio en múltiples fragmentos de muy corta duración y reproducirlos con cierto grado de desorden y solapamiento

Párrafo 4:
- Una limitación significativa de la síntesis granular es que **no** ofrece el mismo control tonal que otros métodos de síntesis ofrecen.
- Métodos tradicionales como la síntesis sustractiva generan ondas basadas en funciones periódicas. Controlar la nota musical de una onda periódica se reduce a una simple multiplicación. Como consecuencia, la nota del sonido resultante siempre coincide con la nota introducida mediante MIDI.
- La síntesis granular, por otro lado, depende de una fuente de audio arbitraria. Muchos sintetizadores granulares permiten transponer la nota de los fragmentos emitidos de acuerdo a cierta entrada MIDI. Uno puede trabajar de este modo siempre y cuando la fuente contenga una sola nota a lo largo de su duración. Cualquier variación en la nota de la fuente nos forzaría a recalibrar la transposición de manera proporcional a dicha variación, caso contrario, la nota resultante diferiría de la entrada MIDI, causando disonancia indeseada en contextos musicales.

Párrafo 5 (no va):
- Un diseñador de sonido podría eludir este problema prescindiendo totalmente de la transposición y, en su lugar, dividiendo la fuente en "regiones" donde la misma nota se mantiene. Cada posible nota de entrada estaría restringida a las regiones con las que coincide.
- Esta solución no solo es ardua, sino que tambien depende de la fuente. Si la fuente presenta solo tres notas, solo esas podrán ser tocadas, tocar cualquier otra nota resultará en silencio.
- Más aún, adaptar dicha solución para soportar regiones polifónicas, es decir, con más de una nota a la vez, requeriría lógica que posiblemente escapa la expertiz de un diseñador de sonido.

---

Párrafo 1
- Es una necesidad común de compositores recurrir a instrumentos virtuales debido a lo caro que suele ser conseguir y grabar instrumentos reales
- Instrumentos virtuales realistas son difíciles de hacer: grabar muchas variaciones de cada nota y a distintas intensidades (sampling), y armar un script que relacione estos atributos con cada grabación

Párrafo 2
- Contextos musicales contemporáneos, desde bandas sonoras modernas a música pop, son cada vez más abiertos a instrumentos sintéticos o híbridos, no necesariamente realistas, que rompen la barrera entre sampling y síntesis.
- Tradicionalmente, la síntesis mediante tabla de ondas ha sido usada para convertir muestras breves de instrumentos en instrumentos virtuales. Sin embargo, tocar diferentes notas implica estirar la onda de la muestra, lo cual genera pérdida de frecuencias altas (high-end) al tocar notas graves.
- Trabajos más recientes utilizan redes neuronales para convertir breves muestras de audio en presets de sintetizadores. Ya que estos sintetizadores generan ondas proceduralmente, se evita la pérdida de fidelidad producto de estirar ondas existentes. No obstante, el tamaño del espacio de parámetros de estos sintetizadores suele limitar la diversidad de timbre de la emulación resultante, siendo a menudo repetitiva/monótona.

Párrafo 3
- La síntesis granular, particularmente en su forma concatenativa, ha sido descrita como prometedora. Al igual que la síntesis por tabla de ondas, trabaja directamente sobre las muestras y preservando su timbre. Sin embargo, dado que se enfoca en reconstruir un sonido objetivo, su flujo de trabajo es más similar al de un vocoder que de un instrumento virtual. Más aún, la calidad de sus resultados depende del tamaño de su base de datos de muestras (corpus).
- En contraste, formas más comerciales de síntesis granular trabajan sobre muestras singulares en lugar de colecciones grandes. Buena parte de ellos permiten transponer el pitch de la salida de acuerdo a entrada MIDI. No obstante, esta transposición es uniforme. Si existen variaciones de pitch en la muestra, el pitch de salida también diferirá de la nota introducida, haciendo muy difícil trabajar con muestras melódicas.

Párrafo 4
- Incluso afinando previamente la muestra para que tenga un solo pitch, si la variación de pitch es muy grande y, en consecuencia, la corrección de pitch también lo es, nos encontraríamos con una pérdida de fidelidad similar a la de la síntesis mediante tabla de ondas.
- Más aún, si la muestra es polifónica, sería necesario descomponerla en sus componentes monofónicos antes de afinarla.
- Este análisis pone en evidencia una brecha en la aplicación de la síntesis granular en contextos musicales, más allá de la generación de efectos de sonido, donde es más popular.
