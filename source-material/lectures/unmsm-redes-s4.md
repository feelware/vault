---
tags:
  - "#lecture-notes"
src-date: 2025-04-19
src-author:
  - Winston Ugaz Cachay
src-link:
---
# Redes y Transmisión de Datos: Semana 4

## Niveles del modelo de referencia OSI

### Físico

- mínima unidad de información: bit
- le concierne las características de la señal
- TIA/EIA 568: cableado, recursos físicos 
- TIA/EIA 607: puesta a tierra 
- 3 estándares de centros de datos:
	- TIA 942
	- BICSI 002
	- NTP ISO 22237

### Enlace

- conexión con otra computadora
- mínima unidad de información: trama
- cada trama contiene una **dirección MAC**  (¿cómo se interpreta?)
- dos tecnologías en auge  (¿cómo funcionan?):
	- Ethernet 
		- conmutación  (involucra direcciones MAC)
		- switch
		- comunicación entre hosts
	- WiFi
 - ¿puede una trama viajar de un labo a telemática? ¿debería? 
	- dominio de broadcasting
	- VLAN

diferencia entre:
- router
- switch
- hub

switch capa 2 y capa 3
- aún no profundizar enrutamiento

¿cómo saber qué camino deben seguir los dispositivos de una red para enviarse datos?
- Spanning Tree Protocol (STP): árbol de comunicaciones (profundizar)
- PaGP, LACP: múltiples conexiones entre dos dispositivos (¿bucles?)

descargar hoja técnica de equipo de comunicaciones y ver qué estándares soporta
- colas de tráfico de un switch (priorización) (IEEE 802.1X)

#### WiFi

- ¿cómo hace uso del espectro radiológico?
- IEEE-802.11A
- ¿cualquier dispositivo móvil se puede conectar a cualquiera de estas redes? (profundizar)
- características básicas del WiFi
- ¿qué hace posible poder visualizar una red WiFi en la lista de redes disponibles de un celular?
- ¿se puede ocultar dicha red de dicha lista?
- ¿se puede intervenir una red WiFi?
- características de seguridad

### Red

- mínima unidad de información: paquete
	- contiene dirección IP
- enrutamiento vs conmutación
- no hay tramas en [red](#Red)
- no hay paquetes en [enlace](#Enlace)
- ¿es VLAN capa 3?
- ¿conmutador (switch) funciona en capa 2 o capa 3? (en la práctica)
- protocolos de enrutamiento
	- RIP V2
	- OSPF
	- BGP
- tabla de direcciones MAC
- tormenta de broadcast
	- VLAN soluciona esto. Funciona como "paredes" que aislan "cuartos" (dominios de broadcast), donde cada uno de estos cuartos habla un idioma distinto. El enrutador funciona como el traductor
- IP
- **Máscara**
- Gateway/Puerta de enlace
- DNS
- **DHCP**

Subnetting: Operaciones lógicas con IP y máscara

### Transporte

- Mínima unidad de información: segmento
- TCP
- UDP
- IANA port (0-65535)
- sockets

¿puede un DHCP comunicarse con VLANs?

---

- Tema final: VoIP (temas hacia atrás)
- ¿en qué capas operan Ethernet y WiFi?
- **Consultar biblografía**
