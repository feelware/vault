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

---

Párrafo 5 (no va):
- Un diseñador de sonido podría eludir este problema prescindiendo totalmente de la transposición y, en su lugar, dividiendo la fuente en "regiones" donde la misma nota se mantiene. Cada posible nota de entrada estaría restringida a las regiones con las que coincide.
- Esta solución no solo es ardua, sino que tambien depende de la fuente. Si la fuente presenta solo tres notas, solo esas podrán ser tocadas, tocar cualquier otra nota resultará en silencio.
- Más aún, adaptar dicha solución para soportar regiones polifónicas, es decir, con más de una nota a la vez, requeriría lógica que posiblemente escapa la expertiz de un diseñador de sonido.