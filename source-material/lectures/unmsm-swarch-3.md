---
src-date: 2025-01-21
src-author:
  - Manuel Ibarra
src-link: "[[pdf/unmsm-swarch-3.pdf|unmsm-swarch-3]]"
---
# Arquitectura de software: Semana 3

## Arquitectura por capas

- Cada capa tiene una responsabilidad específica

### Arquitectura de dos capas

1. Capa cliente: Interfaz de usuario
2. Capa servidor: Lógica de negocio y gestión de datos

### Arquitectura de tres capas

1. Capa de presentación
2. Capa de lógica de negocio
3. Capa de acceso a datos

Lógica de negocio y acceso a datos son realizados en servidores distintos.

![](../../utilities/attachments/Pasted%20image%2020250121175142.png)

### Arquitectura de cuatro capas

1. Capa de presentación
2. Capa de lógica de negocio
3. **Capa de servicio**: #wip
4. Capa de acceso a datos

![](../../utilities/attachments/Pasted%20image%2020250121175553.png)

### Arquitectura de $N$ capas

Permite añadir capas extra:
- Capa de aplicación: #wip
- Capa de integración: #wip
- Capa de seguridad
- Capa de auditoría y log

Más capas implica más documentación y más pruebas.

![](../../utilities/attachments/Pasted%20image%2020250121180401.png)
