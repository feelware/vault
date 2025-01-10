---
tags:
  - "#lecture-notes"
src-date: 2024-09-23
src-author:
  - Gustavo Arredondo
src-link: Databases I
---
# Databases I - Sesión 12

## Views

![Pasted image 20241111134224](../../utilities/attachments/Pasted%20image%2020241111134224.png)

Nota: La mayoría de veces se barre sobre las tablas **de movimiento**

### Casos de uso

- Crear versiones "públicas" de ciertas tablas que no contenga info sensible
![Pasted image 20241111135053](../../utilities/attachments/Pasted%20image%2020241111135053.png)

- Mostrar info agregada
![Pasted image 20241111135427](../../utilities/attachments/Pasted%20image%2020241111135427.png)

### Consideraciones

- Generalmente no se puede usar `ORDER BY`

### Vistas materializadas

- Realmente almacenan información
- Se actualizan cada cierto tiempo o cuando ocurren cambios en las tablas originales
- Tiempos de respuesta cortos
![Pasted image 20241111141636](../../utilities/attachments/Pasted%20image%2020241111141636.png)
- Actualizar una tabla: `REFRESH` #wip

## Triggers

- Similar a event listeners, reaccionan a
	- cambios específicos (`CREATE`, `SELECT` o `UPDATE`)
	- en tablas o vistas específicas
	- ejecutando una acción específica
	- inmediatamente antes o después de dichos cambios
- Se suelen usar para:
	- actualizar datos derivados
	- crear logs (auditoria)
	- validar datos antes de su inserción

### Consideraciones

- Problemas de performance si la acción es muy compleja o se ejecuta muy frecuentemente
- Difíciles de depurar