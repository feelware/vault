---
tags:
  - "#lecture-notes"
src-date: 2025-04-08
src-author:
  - Juan Gamarra Moreno
src-link: "[[../../source-material/lectures/pdf/unmsm-db2-s3.pdf|unmsm-db2-s3]]"
---
# Bases de Datos 2: Semana 3

- Full Table Scan: Ocurre al hacer una búsqueda `WHERE <columna> = <valor>` cuando no se ha creado un índice para `<columna>`

|            | Búsqueda exacta |
| ---------- | --------------- |
| Sin índice | $O(n)$          |
| B/B+ tree  | $O(\log n)$     |
| Hash table | $O(1)$          |

- Índice clusterizado: #wip
- Índice compuesto: sobre más de una columna

Índice: (nombre, apellido) sirve para ordenar por:
- ✅ nombre
- ✅ nombre, apellido
- ❌ apellido, nombre

## Comparación de distintos tipos de índice

| Índice     | auto? | permite duplicado? | ordena físicamente? | cuantos por tabla? (máximo) |
| ---------- | ----- | ------------------ | ------------------- | --------------------------- |
| primario   | ✅     | ❌                  |                     | 1                           |
| secundario |       | ✅                  |                     | ♾                           |
|            |       |                    |                     |                             |
|            |       |                    |                     |                             |
|            |       |                    |                     |                             |

#wip

## Árbol B vs Árbol B+

|                            | Árbol B | Árbol B+ |
| -------------------------- | ------- | -------- |
| Claves en nodos internos   | ✅       | ✅        |
| Claves en nodos hoja       | ✅       | ✅        |
| Enlaces entre hoja         | ❌       | ✅        |
| Búsqueda secuencial rápida | ❌       | ✅        |

# Árbol B+ vs Hash table

|                     | Árbol B+      | Hash table    |
| ------------------- | ------------- | ------------- |
| Búsqueda exacta     | Rápido        | Muy rápido    |
| Búsqueda por rango  | Eficiente     | No soportado  |
| `ORDER BY`          | Eficiente     | No soportado  |
| Acceso secuencial   | #wip          | #wip          |
| Inserción y borrado | Eficiente     | Muy eficiente |
| Común en DBMS       | Muy frecuente | Limitado      |


> [!note] Nota
> No conviene crear índices en las siguientes situaciones:
> - Tablas pequeñas (ej. Tablas de países). Conviene hacer full-table scan
> - Tablas con alta frecuencia de inserción (ej. Lecturas de sensores)
> - Columnas con muchos valores repetidos (ej. sexo, estado civil)

## Sentencia `EXPLAIN`

Permite ver:
- Si se usa o no índice
- Tipo de acceso (full-scan, index scan, etc)
- Costo estimado

> [!question]
> Dados los siguientes índices:
> - índice(a.paterno, a.materno, nombres)
> - índice(a.materno, nombres)
> - índice(nombres)
>   
> ¿Qué índice conviene usar para ordenar por a.paterno, nombres?

Tomar en cuenta reindexación periódica (`VACUUM`, etc)
