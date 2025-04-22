---
tags:
  - "#lecture-notes"
src-date: 2025-04-05
src-author:
  - Winston Ugaz Cachay
src-link:
---
# Redes y Transmisión de Datos: Semana 2

- Confidencialidad
- Integridad
- Disponibilidad

#wip

¿qué medio de transmisión usar? depende de:
- condiciones de instalación
- volumen de bits transportados por unidad de tiempo
- distancia que los datos pueden recorrer sin sufrir atenuación
- costos (cobre es más barato)

> [!attention] investigar
> - 100 Gigabit Ethernet (solo para quienes exponen sobre Ethernet)
> - Demostrar cual conexión es más rápida:
>   - Miami - Perú
>   - Perú - Brazil

- Cables LS2H #wip
- Protocolos arman "mentalmente" árbol de red

> [!attention] investigar
> - [Dominio de difusión](https://en.wikipedia.org/wiki/Broadcast_domain)

## Hardware de red

#wip

### Router

### Bridge

### Switch

### Gateway

### Network interface controller (NIC)

### Modem

### Hub

> [!attention] investigar
> - voltaje de señales para redes
> - power over ethernet
> - cisco 7604 router

## Tipos de red de acuerdo a escala

- PAN: Espacio personal
- LAN: Dispositivos en una misma residencia (ej. Facultad)
- CAN: Campus
- MAN: Ciudad
- WAN: Geográficamente disperso (ej. Todas las sedes de la UNMSM en el Perú)

## Topología de la red

- Mapa de las conexiones entre dispositivos de una red
- Importante, junto con inventario de la red

### Topología de bus

![](../../utilities/attachments/Pasted%20image%2020250411181039.png)

### Topología de malla completa

- Lógicamente se puede hacer, pero en la práctica es costoso

![](../../utilities/attachments/Pasted%20image%2020250411183214.png)

### Red celular

- Superposición de canales: mínimo 20%

![](../../utilities/attachments/Pasted%20image%2020250411184108.png)

### Red estrella

- Más popular hoy

![](../../utilities/attachments/Pasted%20image%2020250411184720.png)

## Nodos de transmisión

- semi-duplex: bidireccional, pero solo un sentido a la vez (A -> B o B -> A). (ej. Nextel)
- full-duplex: bidireccional todo el tiempo (A <-> B)
