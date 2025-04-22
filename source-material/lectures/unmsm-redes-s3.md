---
tags:
  - "#lecture-notes"
src-date: 2025-04-19
src-author:
  - Winston Ugaz Cachay
src-link:
---
# Redes y Transmisión de Datos: Semana 3

## Capas del modelo de referencia OSI

### Física

- mínima unidad de información: bit
- le concierne las características de la señal
- TIA/EIA 568: cableado, recursos físicos #hw
- TIA/EIA 607: puesta a tierra #hw

### Enlace

- conexión con otra computadora
- unidad de información: trama
- cada trama contiene una **dirección MAC** #hw (¿cómo se interpreta?)
- dos tecnologías en auge #hw (¿cómo funcionan?):
	- Ethernet #hw
		- conmutación #hw (involucra direcciones MAC)
		- switch #hw
		- comunicación entre hosts #hw
	- WiFi
 - ¿puede una trama viajar de un labo a telemática? ¿debería? #hw
	- dominio de broadcasting #hw
	- VLAN

#hw diferencia entre:
- router
- switch
- hub

- switch capa 2 y capa 3 #hw
- aún no profundizar enrutamiento

¿cómo saber qué camino deben seguir los dispositivos de una red para enviarse datos?-
- STP: árbol de comunicaciones #hw (profundizar)
- 