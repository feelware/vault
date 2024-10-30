---
tags:
  - "#lecture-notes"
src-date: 2024-09-16
src-author:
  - Gustavo Arredondo
src-link: Databases I
---
# Databases I - Session 5

## SQL: Tipos de datos

- SQL Server: Money, XML

## Clasificación de comandos SQL

### DDL: Definición de datos

- Construcción (`CREATE`), edición (`ALTER`) y eliminación (`DROP`) de objetos (bases de datos, tablas, vistas, índices, etc.)
- Modifican estructura de DB

#### Create

```sql

```

### DML: Manipulación de datos (CRUD)

#### Insert

```sql
INSERT INTO employees (name, age, active)
VALUES ('Juan', 26, true),
       ('Ana', 24, false),
       ('Pedro', 34, true);
```

#### Update

```sql
UPDATE employees
SET active = false
WHERE age > 60;
```

#### Delete

```sql
DELETE FROM employees
WHERE active = false;
```

### DQL: Obtención de datos

#### `SELECT`

```sql
SELECT * FROM employees;
```

```sql
SELECT name, age
FROM employees
WHERE age < 30;
```

### DCL: Control de acceso

#### `GRANT`

#### `REVOKE`

### TCL: Control de transacciones

- Transacciones: Lista de tareas que se ejecutan de inicio a fin
- Si alguna de las tareas falla, la transacción es completamente revertida 

#### `BEGIN TRANSACTION`

#### `COMMIT`

#### `ROLLBACK`

#### `SAVEPOINT`

## Cláusulas SQL

### `WHERE`

- Filtra filas en base a una condición

```sql
SELECT first_name, last_name, gender
FROM patients
WHERE gender = 'M';
```

### `BETWEEN`

- Expresa rangos de valores
```sql
SELECT first_name, last_name
FROM patients
WHERE weight BETWEEN 100 AND 120;
```

- Alternative:
```sql
SELECT first_name, last_name
FROM patients
WHERE weight <= 120 and weight >= 100;
```

### `LIKE`

```sql
SELECT first_name
FROM patients
WHERE first_name LIKE 'C%'
```

### `GROUP BY`

- Agrupa filas según algún atributo

### `HAVING`

- Filtra grupos en base a una condición

### `ORDER BY`

- Ordenar ascendente o descendentemente según atributo especificado

### `LIMIT`

- Limita cantidad de resultados

### `OFFSET`

- Desplaza el punto de inicio

### `DISTINCT`

- Devuelve solo resultados que no se repiten

```sql
SELECT DISTINCT email
FROM employees
```

## Funciones

### `COUNT`

```sql
SELECT COUNT(*)
FROM patients
AS total_patients
WHERE YEAR(birth_date) = 2010;
```

### `CONCAT` 

```sql
SELECT CONCAT('one ', 'two ', 'three') AS numbers
```

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM patients
```

	