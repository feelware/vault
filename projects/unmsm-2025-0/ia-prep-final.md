---
status: doing
deadline: 2025-07-10T00:00
class: ia
---
Los temas que se consideran para el examen final, tanto la parte conceptual como la práctica, son:

- [ ] Clasificación
	- [x] kNN
	- [ ] Regresión logística
	- [x] SVM
	- [ ] Medidas de evaluación en problemas de clasificación
- [ ] PMC-BP
- [ ] c-means (aprendizaje no supervisado)

## kNN y regresión logística

- [unmsm-ia-clas](../../source-material/lectures/pdf/unmsm-ia-clas.pdf)

para cierto punto de clase desconocida, se elige la clase más popular entre los k vecinos más cercanos (por distancia euclidiana)

## SVM

- [unmsm-ia-svm](../../source-material/lectures/pdf/unmsm-ia-svm.pdf)

Clasifica puntos n-dimensionales en dos grupos

Cada hiperplano puede representarse como el conjunto de puntos $n$-dimensionales, de los cuales cada punto $\mathbf{x}$ satisface la siguiente ecuación:
$$
\mathbf{w}^T\mathbf{x} + b
= \begin{bmatrix}
w_1 \ w_2 \ w_3 \ ... \ w_p
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2 \\
x_3 \\
... \\
x_p
\end{bmatrix}
+ b
= w_1 x_1 + x_2 x_2 + w_3 x_3 + ... + w_p x_p + b
= 0
$$
Donde $\mathbf{w}^T$ es la transpuesta del vector de coeficientes que se busca optimizar y $b$ es el sesgo.

Podemos saber si cierto punto $\mathbf{x}$ está "arriba", "abajo" o "dentro" del hiperplano evaluando $\mathbf{w}^T\mathbf{x} + b$.
- Si el resultado es positivo, $\mathbf{x}$ está arriba (clase positiva)
- Si es menor, $\mathbf{x}$ está abajo (clase negativa)
- Si es cero, $\mathbf{x}$ es parte del hiperplano

Podemos saber la distancia de $p$ al hiperplano con la siguiente fórmula:
$$
d = \dfrac{|\mathbf{w}^T\mathbf{p} + b|}{\sqrt{\sum_i w_i^2}}
$$
- Solo los vectores de soporte influencian el hiperplano escogido, no el resto de puntos

## Medidas de evaluación

- [unmsm-ia-clas-eval](../../source-material/lectures/pdf/unmsm-ia-clas-eval.pdf)

## PMC-BP

- [unmsm-ia-rna-p1](../../source-material/lectures/pdf/unmsm-ia-rna-p1.pdf)
- [unmsm-ia-rna-p2](../../source-material/lectures/pdf/unmsm-ia-rna-p2.pdf)
- [ejercicio](../../source-material/lectures/pdf/unmsm-ia-rna-ej-res.pdf)

## c-means

- [unmsm-ia-c-means](../../source-material/lectures/pdf/unmsm-ia-c-means.pdf)
