---
tags:
  - "#lecture-notes"
src-date: 
src-author:
  - Juan Gamarra Moreno
src-link: "[[pdf/unmsm-db2-s5.pdf|unmsm-db2-s5]]"
---
# Base de Datos 2: Semana 5

- Consulta: declarativa
- Ejecución: imperativa

## Optimizador de consultas

- componente del DBMS
- examina árbol lógico de consulta
- genera planes de ejecución posibles
- calcula costo estimado (tiempo, I/O, CPU, memoria)
- selecciona plan con menor costo

### Tipos de optimizadores

- basado en reglas: heurísticas fijas
- basado en costos: estadísticas y modelos

> [!note]
> si índices están desactualizados, el optimizador puede tomar malas decisiones

## Etapas del Procesamiento Interno de una Consulta

### Análisis léxico y sintáctico

- Análisis léxico: tokenizing (SELECT, nombre, salario, FROM, empleados, WHERE, salario, >, 5000)
- Análisis sintáctico: construcción del árbol de sintaxis ![](../../utilities/attachments/Pasted%20image%2020250423175823.png)

### Re-escritura lógica de la consulta

Transformación del árbol de sintáxis

- eliminación de sub-consultas innecesarias
- push-down de predicados
- unificación de joins y filtros

### Generación de planes físicos de ejecución

#wip

### Selección del mejor plan

#wip

## Estrategias de Evaluación de Operadores Relacionales

### Selección

#wip

### Proyección

Reducción de columnas #wip

### Join

- Nested loop join: $O(n^2)$
- Merge join: Tablas deben estar ordenadas por clave de join
- Hash join: #wip

### Agregación

- Hash table aggregation
- Tree-based aggregation
- Sort-based aggregation

> [!note]
> cardinalidad: filas afectadas por la consulta

## Evaluación de rendimiento

#wip
