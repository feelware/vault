---
status: done
deadline: 2025-05-09T22:00
class: redes
---
- [ ] Leer capítulo 7
- [ ] Leer capítulo 11 (LAN)
- [ ] Repasar protocolos MAC (ALOHA, CSMA, CSMA/CD)
- [ ] Investigar Ethernet moderno y transición a topología estrella (switches)
- [ ] Repasar MAC frame

---

Ideas:
- Empezar recordando que Ethernet comprende dos capas: física y de enlace
- Recordar que, en LANs, capa de enlace está divida en LLC y MAC. Explicar qué ofrece Ethernet en particular para cada una de estas capas
- Al explicar MAC, y en concreto CSMA/CD, empezar diciendo que es más fácil entenderlo si se observa primero los precursores (ALOHA y CSMA)
- Continuar con expo anterior. Al terminar, recordar que transición a switches hace a CSMA/CD algo obsoleto

## Data Link Layer

Arbitrates a medium shared by a (local) network of devices:

> The data link layer is concerned with local delivery of [frames](https://en.wikipedia.org/wiki/Frame_\(networking\) "Frame (networking)") between nodes on the same level of the network. Data-link frames, as these [protocol data units](https://en.wikipedia.org/wiki/Protocol_data_unit "Protocol data unit") are called, do not cross the boundaries of a local area network. Inter-network routing and global addressing are higher-layer functions, allowing data-link protocols to focus on local delivery, addressing, and media arbitration. In this way, the data link layer is analogous to a neighborhood traffic cop; **it endeavors to arbitrate between parties contending for access to a medium, without concern for their ultimate destination**. When devices attempt to use a medium simultaneously, frame collisions occur. Data-link protocols specify how devices detect and recover from such collisions, and may provide mechanisms to reduce or prevent them.

The protocols of the data link layer:

- Respond to service requests from the [network layer](https://en.wikipedia.org/wiki/Network_layer "Network layer")
- Issue service requests to the [physical layer](https://en.wikipedia.org/wiki/Physical_layer "Physical layer")

These transfers may be unreliable.

- Many data link protocols do not have acknowledgments of successful frame reception and acceptance
- Some data link protocols might not even perform any check for transmission errors
- In those cases, higher-level protocols must provide [flow control](https://en.wikipedia.org/wiki/Flow_control_\(data\) "Flow control (data)"), error checking, acknowledgments, and retransmission.

## LLC vs MAC

> The LLC provides [flow control](https://en.wikipedia.org/wiki/Flow_control_\(data\) "Flow control (data)") and [multiplexing](https://en.wikipedia.org/wiki/Multiplexing "Multiplexing") for the **logical link** (i.e. [EtherType](https://en.wikipedia.org/wiki/EtherType "EtherType"), [802.1Q VLAN tag](https://en.wikipedia.org/wiki/802.1Q_VLAN_tag "802.1Q VLAN tag") etc), while the MAC provides flow control and multiplexing for the **transmission medium**.

### LLC

- [Multiplexes](https://en.wikipedia.org/wiki/Multiplexing) protocols running at the top of the data link layer
- Specifies which mechanisms are to be used for addressing stations over the transmission medium and for controlling the data exchanged between the originator and recipient machines
- Optionally provides:
	- [Flow control](https://en.wikipedia.org/wiki/Flow_control_\(data\) "Flow control (data)"), in addition to the one provided on the [transport layer](https://en.wikipedia.org/wiki/Transport_layer "Transport layer")
	- [Error control](https://en.wikipedia.org/wiki/Error_control) ([automatic repeat request](https://en.wikipedia.org/wiki/Automatic_repeat_request "Automatic repeat request"), ARQ), in addition to ARQ provided by some [transport-layer protocols](https://en.wikipedia.org/wiki/Transport-layer_protocol "Transport-layer protocol"), to [forward error correction](https://en.wikipedia.org/wiki/Forward_error_correction "Forward error correction") (FEC) techniques provided on the [physical layer](https://en.wikipedia.org/wiki/Physical_layer "Physical layer"), and to error-detection and packet canceling provided at all layers, including the [network layer](https://en.wikipedia.org/wiki/Network_layer "Network layer")

### MAC

- Determines who is allowed to access the media at any one time (e.g. [CSMA/CD](https://en.wikipedia.org/wiki/Carrier-sense_multiple_access_with_collision_detection "Carrier-sense multiple access with collision detection"))
- Performs [frame synchronization](https://en.wikipedia.org/wiki/Frame_synchronization "Frame synchronization"), which determines the start and end of each frame of data in the transmission [bitstream](https://en.wikipedia.org/wiki/Bitstream "Bitstream")
- Physical addressing ([MAC addressing](https://en.wikipedia.org/wiki/MAC_address "MAC address"))
- [LAN switching](https://en.wikipedia.org/wiki/LAN_switching "LAN switching") ([packet switching](https://en.wikipedia.org/wiki/Packet_switching "Packet switching")), including [MAC filtering](https://en.wikipedia.org/wiki/MAC_filtering "MAC filtering"), [Spanning Tree Protocol](https://en.wikipedia.org/wiki/Spanning_Tree_Protocol "Spanning Tree Protocol") (STP), [Shortest Path Bridging](https://en.wikipedia.org/wiki/Shortest_Path_Bridging "Shortest Path Bridging") (SPB) and [TRILL](https://en.wikipedia.org/wiki/TRILL "TRILL") (TRansparent Interconnection of Lots of Links)
- Data packet queuing or [scheduling](https://en.wikipedia.org/wiki/Scheduling_algorithm#In_computer_networks_and_multiplexing "Scheduling algorithm")
- [Store-and-forward](https://en.wikipedia.org/wiki/Store-and-forward "Store-and-forward") switching or [cut-through switching](https://en.wikipedia.org/wiki/Cut-through_switching "Cut-through switching")
- [Quality of service](https://en.wikipedia.org/wiki/Quality_of_service "Quality of service") (QoS) control
- [Virtual LANs](https://en.wikipedia.org/wiki/Virtual_LAN "Virtual LAN") (VLAN)

## Implementation of LLC and MAC on Ethernet

### LLC

- Doesn't do error control.

> Data-link-layer error control (i.e. re-transmission of erroneous packets) is provided in wireless networks and [V.42](https://en.wikipedia.org/wiki/ITU-T_V.42 "ITU-T V.42") telephone network modems, **but not in LAN protocols such as [Ethernet](https://en.wikipedia.org/wiki/Ethernet "Ethernet")**, since **bit errors are so uncommon in short wires**. In that case, only [error detection](https://en.wikipedia.org/wiki/Error_detection "Error detection") and canceling of erroneous packets are provided.

- Doesn't do flow control.

> **Data-link-layer flow control is not used in LAN protocols such as Ethernet**, but in modems and wireless networks.

Most modern protocols (like IP) prefer **Type 1 LLC** or bypass LLC altogether by using **Ethernet II framing**, which doesn’t involve LLC headers at all. The **complexity of Type 2 (connection-mode)** and **Type 3 (acknowledged connectionless)** makes them impractical — most of their roles are now filled by **Layer 3 (IP)** and **Layer 4 (TCP/UDP)**.

### MAC

- Multiple access method: [CSMA/CD](https://en.wikipedia.org/wiki/Carrier-sense_multiple_access_with_collision_detection "Carrier-sense multiple access with collision detection") protocols for [collision detection](https://en.wikipedia.org/wiki/Collision_detection "Collision detection") and re-transmission in Ethernet bus networks and hub networks

---

Debo realizar una exposición sobre los fundamentos de Ethernet clásico, en el contexto de una exposición grupal sobre Ethernet. Aquí está la estructura a grandes rasgos/lineamientos sobre el orden de mi exposición:

# LLC y MAC: Fundamentos de Ethernet clásico

- Ethernet comprende dos capas: física y de enlace (LLC y MAC)
- La capa física se explicará más adelante
- Para entender mejor diferencia de responsabilidades de LLC y MAC, expondremos la estructura de una trama Ethernet

## Estructura de una trama de Ethernet

- La estructura de esta trama ha sufrido cambios ligeros pero importantes

### Preamble + SFD

- 8 bits
- Ráfaga de unos y ceros (sincronización)

### Direcciones MAC (Source y Destination)

- Ambos de seis bits
- Direcciones únicas ($2^{24}$ direcciones por fabricante)
- Último bit de Destination: multicasting
- Más adelante se brindarán detalles sobre cómo son usadas para conmutación

### Type/Length

- En tramas tipo Ethernet:
	- Indica a qué protocolo de red redirigir la trama (Type)
	- Ejemplo: 0x0800 corresponde a IPv4
- En tramas tipo IEEE 802.3:
	- Se nota un problema: no es posible saber el tamaño de un frame sin inspeccionar el payload (**violación de capa**)
	- Type field pasa a **Length** field
	- Especificación de protocolo de red es delegada a LLC (DSAP y SSAP)
- Muchos fabricantes ya se habían acomodado a estándar original
- IEEE finalmente acepta a ambos usos como válidos
	- Valor ≤ 1500: Length (se trata de un frame IEEE)
	- Valor ≥ 1536: Type (se trata de un frame Ethernet)
- Hoy en día, tramas tipo Ethernet 2 predominan: LLC ya no se usa para indicar protocolos de red
- Recordemos los tres servicios ofrecidos por LLC (tipos 1, 2 y 3)
- Dado que cableado físico es relativamente confiable, solo tipo 1 (unacknowledged connectionless) es usado
- Tipo 1 no ofrece control de flujo ni control de errores
- Así, **LLC está relativamente obsoleto en el Ethernet moderno**

### Payload

- Data que viene de la capa superior
- Límite superior de 1500 bytes tiene razones históricas
- Límite inferior de 46 bytes existe para evitar colisiones por frames pequeños
- Si se tiene menos de 46 bytes, padding es usado

### Checksum

- CRC de 4 bytes
- No hace corrección de errores, solo detección y descarte

## CSMA/CD: Arbitrando el medio

### Antecedentes

#### Pure y slotted ALOHA

- Pure: Enviar frames cuando sea que estén listos
- Slotted: Enviar frames tras un ciclo de reloj unánime
- Ambas soluciones, a pesar que salvaron el día, fueron algo apresuradas

#### CSMA

- Se aprovecha que, en LANs, es posible escuchar el canal y adaptarse a lo que está ocurriendo
- Este nuevo enfoque trae consigo nuevos desafíos
- Persistencia: ¿Qué hacer cuando el canal está ocupado?
	- 1-persistent: Quedarse escuchando hasta que se desocupe (agresivo)
	- non-persistent: Si está ocupado, esperar un momento para volver a intentar (pasivo)
	- p-persistent: Decidir bajo cierta probabilidad si transmitir o esperar por un tiempo (inteligente, pero no escala)

## Funcionamiento

- Mejora sustancial: No solo escuchar antes de transmitir, sino también *mientras* se transmite
- Si detecta un nivel de voltaje anómalo, se asume una colisión
- La transmisión es detenida inmediatamente
- Se avisa a la red sobre la colisión (jamming)
- Se espera por un tiempo aleatorio antes de volver a intentar (si el canal está libre)
- CSMA/CD es 1-persistent: Envía tan pronto el medio esté libre
- Esto no es tan problemático porque:
	- Si vuelve a ocurrir una colisión entre los mismos hosts, el tiempo de espera se incrementa exponencialmente
	- En general, se intenta que las tramas sean lo suficientemente grandes para evitar colisiones
- En redes inalámbricas, este enfoque es inviable, pues hay mucho decaimiento de voltaje, en este caso se usa CSMA/CA

## ¿Sigue siendo CSMA/CD relevante?

- Ethernet moderno es casi completamente distinto
- Predomina topología estrella, en lugar de bus
- Switches full-duplex hacen que cada puerto sea su propio **dominio de colisión**
- Sin colisiones, CSMA/CD queda obsoleto

Citas relevantes:

> Unacknowledged connectionless service (type 1) consists of having the source machine send independent frames to the destination machine without having the destination machine acknowledge them. Ethernet is a good example of a data link layer that provides this class of service. No logical connection is established beforehand or released afterward. If a frame is lost due to noise on the line, no attempt is made to detect the loss or recover from it in the data link layer.

> For unacknowledged connectionless service it might be fine if the sender just kept outputting frames without regard to whether they were arriving properly.

> Ethernet uses a Type field to tell the receiver what to do with the frame. Multiple network-layer protocols may be in use at the same time on the same machine, so when an Ethernet frame arrives, the operating system has to know which one to hand the frame to. The Type field specifies which process to give the frame to. For example, a type code of 0x0800 means that the data contains an IPv4 packet. IEEE 802.3, in its wisdom, decided that this field would carry the length of the frame, since the Ethernet length was determined by looking inside the data—a layering violation if ever there was one. Of course, this meant there was no way for the receiver to figure out what to do with an incoming frame. That problem was handled by the addition of another header for the LLC (Logical Link Control) protocol within the data. It uses 8 bytes to convey the 2 bytes of protocol type information. Unfortunately, by the time 802.3 was published, so much hardware and software for DIX Ethernet was already in use that few manufacturers and users were enthusiastic about repackaging the Type and Length fields. In 1997, IEEE threw in the towel and said that both ways were fine with it. Fortunately, all the Type fields in use before 1997 had values greater than 1500, then well established as the maximum data size. Now the rule is that any number there less than or equal to 0x600 (1536) can be interpreted as Length, and any number greater than 0x600 can be interpreted as Type.

> All three LLC protocols employ the same PDU format, which consists of four fields. The DSAP (Destination Service Access Point) and SSAP (Source Service Access Point) fields each contain a 7-bit address, which specifies the destination and source users of LLC. One bit of the DSAP indicates whether the DSAP is an individual or group address. One bit of the SSAP indicates whether the PDU is a command or response PDU. The format of the LLC control field is identical to that of HDLC, using extended (7-bit) sequence numbers.

> For a CSMA/CD LAN, the question arises as to which persistence algorithm to use. You may be surprised to learn that the algorithm used in the IEEE 802.3 standard is 1-persistent. Recall that both nonpersistent and p-persistent have performance problems. In the nonpersistent case, capacity is wasted because the medium will generally remain idle following the end of a transmission even if there are stations waiting to send. In the p-persistent case, p must be set low enough to avoid instability, with the result of sometimes atrocious delays under light load. The 1- persistent algorithm, which means, after all, that p = 1, would seem to be even more unstable than p-persistent due to the greed of the stations. What saves the day is that the wasted time due to collisions is mercifully short (if the frames are long relative to propagation delay), and with random backoff, the two stations involved in a collision are unlikely to collide on their next tries. o ensure that backoff maintains stability, IEEE 802.3 and Ethernet use a technique known as binary exponential backoff. A station will attempt to transmit repeatedly in the face of repeated collisions. For the first 10 retransmission attempts, the mean value of the random delay is doubled. This mean value then remains the same for 6 additional attempts. After 16 unsuccessful attempts, the station gives up and reports an error. Thus, as congestion increases, stations back off by larger and larger amounts to reduce the probability of collision.
