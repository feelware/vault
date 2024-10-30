# Análisis estadístico de la mejora en la identificación de problemas de calidad del producto

- A continuación, veremos qué pruebas fueron realizadas para comprobar si realmente hubo una mejora tras aplicar el modelo propuesto por este estudio. []

## Prueba estadística usada: Prueba T pareada

- Como ya fue mencionado, se realizaron cuatro ciclos de auditoria tanto en el 2017 (**antes** de aplicar de modelo) como en el primer trimestre del 2018 (**después** de aplicar el modelo). []
- En esta tabla se registra cuántos problemas de calidad fueron encontrados en cada año. ![](utilities/attachments/Pasted%20image%2020240918110342.png)
- A simple vista podemos apreciar un **aumento** en la detección de problemas tras introducir el modelo. []
- Si sacamos el promedio de cada periodo y los restamos, obtendremos un aumento promedio de 7.75.
- Pero este número no nos dice mucho por sí mismo []
- ¿Cómo sabemos si esta diferencia realmente **significa** algo? []
- Para determinar esto, se utilizó una **prueba T pareada**. 
- Esta prueba compara dos conjuntos de datos relacionados para ver si la **diferencia promedio** entre ambos es significativa.
- La prueba T es adecuada cuando queremos comparar los promedios de dos muestras tomadas sobre los **mismos** elementos en **diferentes** momentos, lo cuál es precisamente nuestro caso. []

## Hipótesis nula y alternativa

- En el contexto de esta prueba, se plantean dos hipótesis:
- La **hipótesis nula** afirma que la **diferencia media** entre los problemas identificados en ambos periodos es igual a cero.
- En otras palabras, afirma que **NO** ha habido mejora en la identificación de problemas de calidad del producto.
- Por otro lado, la **hipótesis alternativa** afirma que **SÍ** ha habido una mejora en la identificación de problemas. 
- Implicando que la diferencia media entre ambos periodos es distinta de cero. []
- El objetivo del análisis es **rechazar o no rechazar** la hipótesis nula.
- Si los datos proporcionan **suficiente** evidencia, la hipótesis nula será rechazada, y se concluirá que **efectivamente** ha habido una mejora. []

## Proceso

- Veamos ahora la serie de pasos que se sigue para saber si se debe rechazar o no la hipótesis nula.
- Es un proceso relativamente directo, pero compuesto por **varios** pasos secuenciales.
- Primero que nada, necesitamos una lista con todas las diferencias entre los pares análogos presentados en la tabla 6. []
$$
\begin{align}
d_1 = x_1 - y_1 = 5 - 13 = -8 \\
d_2 = x_2 - y_2 = 7 - 14 = -7 \\
d_3 = x_3 - y_3 = 9 - 16 = -7 \\
d_4 = x_4 - y_4 = 9 - 18 = -9 \\
\end{align}
$$
- De esta lista se obtiene la media y la desviación estándar []

$$
\begin{align}
\overline{d} = \dfrac{\sum{d}}{n} = -7.75
\end{align}
$$
$$
\begin{align}
s_d = \sqrt{\dfrac{\sum{(d - \overline{d})^2}}{n-1}}
\end{align}
$$
- De la desviación estándar se obtiene el error estándar de la media []
$$
\begin{align}
SE(\overline{d}) = \dfrac{s_d}{\sqrt{n}}  = 0.479
\end{align}
$$
- Y del error estándar de la media se obtiene el valor T []
$$
\begin{align}
T = \dfrac{\overline{d}}{SE(\overline{d})} = −16.19
\end{align}
$$
- El cuál, en conjunto con los grados de libertad, se usa para encontrar el valor que finalmente nos permitirá saber si se rechaza o no la hipótesis: []
- **el valor p**, el cuál en este caso vale 0.001 []
- ¿Qué nos dice el valor p sobre la validez de la hipótesis?
- Si bien es cierto que en estadística inferencial casi nunca se tiene **completa** certeza sobre la validez de una hipótesis, podemos determinar ciertos **niveles** de confianza en que nuestra inferencia es certera. []
- En este estudio, se estableció un intervalo de confianza de 95%, lo que significa que para rechazar la hipótesis nula necesitamos que el valor p sea **menor** a 0.05 []
- Claramente 0.001 es menor a 0.05, así que podemos rechazar la hipótesis nula con un 95% de confianza.
- En otras palabras, podemos establecer con un 95% de confianza que la aplicación del modelo de aseguramiento de la calidad propuesto por este estudio ha producido mejoras significativas en la identificación de errores de calidad de producto. []