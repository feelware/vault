---
status: doing
deadline: 2025-07-04T23:00
class: redes
---

> [!quote] Tarea original
>
> Desarrollar el tema de VoIP, e implementar una central telefónica basada en asterisk, con demo de llamada.
>
> Importante:
>
> - Explicar los protocolos relacionados a VoIP.
> - **Explicar los codecs utilizados y recomendados.**
> - Explicar los conceptos relacionados a la mejor explotación de una central telefónica corporativa.

- [x] Investigar sobre Asterisk y cómo funciona
- [x] Elaborar guión y diapositivas
- [ ] Estudiar guión
- [ ] Averiguar como probar cambios en la configuración de codecs

---

- [Guión]()

## Outline

- empezar explicando el siguiente punto:
  > Even modest quality, high-fidelity stereo sound can use a substantial amount of disk space. For web developers, an even bigger concern is the **network bandwidth needed** in order to transfer audio, whether for streaming or to download it for use during gameplay. The processing of audio data to encode and decode it is handled by an audio **[codec](https://developer.mozilla.org/en-US/docs/Glossary/Codec)** (**CO**der/**DEC**oder).
- a la fecha han sido creados muchos codecs, algunos abiertos y otros propietarios. en general, la elección de codecs, así como su configuración, depende de **variables** relacionadas al **formato/contenido** que se desea transmitir (voz/música, número de canales, etc) y la naturaleza del **medio de transmisión** (limites de CPU o ancho de banda, compatibilidad con hardware, etc). usar [esta fuente](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Formats/Audio_codecs)
- mostrar algunos codecs populares en ciertos contextos (MP3, FLAC, etc). luego, hacer un contraste mencionando qué codecs son más usados en VoIP (G.711, G.722, y Opus) (usar misma fuente anterior) haciendo un primer énfasis en G.711, uno de los más antiguos (1972) y aún relevantes. mencionar que "para explicar su popularidad, primero debemos entender qué limitaciones y libertades significa un contexto de VoIP"
- recordar naturaleza continua de sonido "real" y necesidad de discretizarlo (muestreo) para ser representable computacionalmente
- explicar que el ser humano puede escuchar cierto rango de frecuencias, y que la tasa de muestreo afecta rango de frecuencias representables (nyquist), por lo que la mayoría del audio digital moderno suele ser ligeramente mayor a 40khz (doble de 20khz, limite superior de audición humana)
  > [...] raw uncompressed [PCM audio](https://en.wikipedia.org/wiki/PCM_audio "PCM audio") (44.1 kHz, 16-bit stereo, as represented on an audio CD or in a .wav or .aiff file) has long been a standard across multiple platforms, but **its transmission over networks is slow** and expensive
- explicar que, a diferencia de la música, la voz no necesita todo el espectro audible para ser inteligible (300 a 3400 hz es aceptable), por lo que la tasa de muestreo no debe ser demasiado alta (G.711 usa una tasa de 8000 hz)
- explicar otro problema: mientras más rango dinámico se requiera (desde susurros a gritos), más "grandes" deben ser los números usados para representar los valores de onda (mayor profundidad de bits)
- explicar proceso de companding (compresión + expansión) para que el rango dinámico original (14 bits) "sobreviva" a la baja profundidad de bits usada durante transmisión (8-bit): la señal pasa por cierta función en el emisor, y luego por la función inversa en el receptor
  - explicar que por razones históricas existen dos variantes (laws): mu-law y A-law. no hay mucha diferencia de calidad, pero cada una emplea funciones distintas: si se comprime con mu-law y expande con A-law (o viceversa), la señal no es restaurada correctamente
- explicar las diferencias sustanciales que ofrece Opus, lanzado el 2012 y adoptado por WebRTC, siendo el codec preferido por plataformas como Discord.
- Explicar por qué a pesar de ser superior que G.711 (Opus sí realiza compresión de datos y utiliza VBR para adaptarse a distintos anchos de banda), muchos siguen prefiriendo G.711, especialmente para redes corporativas/PBX internas
  > it is the highest quality audio encoding which can be transmitted through the public telephone network
- reflexionar sobre qué codec es realmente mejor para VoIP
- mostrar brevemente cómo configurar `/etc/asterisk/codecs.conf`, considerando lo mencionado por la [esta parte](https://docs.asterisk.org/Fundamentals/Asterisk-Architecture/Types-of-Asterisk-Modules/Codec-Modules/) y [esta otra parte](https://docs.asterisk.org/Configuration/Codec-Opus/) de la documentación de Asterisk
