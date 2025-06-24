---
status: done
deadline: 2025-05-02T12:00:00
class: redes
---
# Ethernet Presentation Outline

## 1. Background on Local Area Networks (from Stallings, pp.356–384)

- **LAN definition:** A LAN is typically a private network owned by its organization, with much higher data capacity than a WAN. LANs serve local communication needs and use specific topologies and media.
    
- **Key LAN elements:** The design of a LAN is defined by its _physical topology_, _transmission medium_, _wiring layout_, and _media-access method_. These factors determine cost, capacity, and supported applications.
    
- **Common topologies:** Ethernet’s history began with a shared **bus**. Other LAN topologies include **tree**, **ring**, and (most common today) **star**. In a bus/tree network, all stations attach to the same cable (terminated at each end) so that every transmission reaches all nodes. (For example, a bus is a linear cable with taps and terminators at each end.)
    
- **IEEE 802 LAN architecture:** LANs use a layered model: a physical layer (including the actual medium and topology) and two sublayers at the data link layer – MAC and LLC. The 802.3 standard (Ethernet) follows this model: the physical layer defines the cable and signaling, while the MAC layer handles framing, addressing, and channel access (and the LLC layer provides error/flow control interfaces).
    
- **Addressing and medium access:** Each station has a unique 48-bit MAC address for **Destination** and **Source** fields in frames. In a shared medium (bus or hub), only one frame can be transmitted at a time. Carrier-sense multiple access with collision detection (CSMA/CD) is used to coordinate access on a shared LAN: stations listen first and send when idle, and if collisions occur they stop and retry (details below).
    

## 2. History and Rationale of Ethernet (from Tanenbaum, pp.304–323)

- **Origin (1970s):** Ethernet was invented by Bob Metcalfe and David Boggs at Xerox PARC (Palo Alto Research Center) in the mid-1970s to link the new personal computers there. Metcalfe, influenced by ALOHAnet work, “designed and implemented the first local area network” in 1976 using a long thick coaxial cable at about 3 Mbps. This network connected the otherwise isolated PARC workstations.
    
- **Name:** They called the system _Ethernet_ after the 19th-century concept of the “luminiferous ether” – the hypothetical medium for electromagnetic waves. The term emphasized the idea of a shared broadcast medium for data.
    
- **Standardization:** The early “Xerox Ethernet” proved very successful. In 1978, Digital, Intel, and Xerox (the “DIX” consortium) formalized a 10 Mbps version as the **DIX standard**. A few years later (1983), this became the IEEE 802.3 Ethernet standard. (IEEE 802.3 differs only in minor framing details.)
    
- **Why Ethernet was created:** Ethernet’s creation was motivated by the need for a high-speed LAN to support personal computers and workstations. It provided a simple bus LAN that supported multiple stations without complex central control. After Xerox did not commercialize Ethernet hardware, Metcalfe co-founded 3Com to sell Ethernet network adapters, popularizing Ethernet in PCs.
    

## 3. Ethernet Technical and Architectural Details (from Stallings, pp.385–418)

- **Bus-based architecture:** Traditional Ethernet was a shared-bus or multi-drop cable system. In a bus topology (or with repeater hubs), all stations share one medium. A hub repeats any incoming signal to all other ports, making the network _physically a star_ but _logically a bus_. This means every transmission is seen by all stations, and only one frame may be on the medium at once.
    
- **Ethernet frame format:** Ethernet frames consist of: a 7-byte **preamble** (alternating 0/1 for sync) and 1-byte Start Frame Delimiter; a 6-byte **Destination Address** and 6-byte **Source Address**; a 2-byte **Length/Type** field; the payload data (46–1500 bytes, with padding if needed for minimum length); and a 4-byte **Frame Check Sequence (CRC)**. (If the Length/Type field ≥1536, it identifies the upper-layer protocol by type; otherwise it is a payload length.) The minimum Ethernet frame size (64 bytes) ensures that collisions are detected. The 48-bit MAC addresses in DA/SA uniquely identify network interfaces.
    
- **MAC protocol – CSMA/CD:** Ethernet uses _Carrier Sense Multiple Access with Collision Detection_. Before sending, a station listens to ensure the medium is idle. If idle, it transmits immediately; if busy, it waits for silence. If two stations transmit simultaneously, their signals collide and corrupt each other. Upon detecting a collision, each sender immediately stops, transmits a brief jamming signal (to notify others), and then waits a random backoff interval before retrying. This random (binary exponential) backoff reduces the chance of repeated collisions. Thus, Ethernet implements a four-step procedure: listen, transmit if idle; if collision, stop and back off; then retry.
    
- **Physical layer variants:** The original Ethernet (10BASE5) used thick coaxial cable (up to 500 m per segment) with Manchester encoding. A later variant (10BASE2) used thinner “cheapernet” coax (up to 185 m). Both are baseband shared media. Each segment could be extended by repeaters, but all segments remained one collision domain. (IEEE 802.3 later added twisted-pair and fiber options.)
    

## 4. Advances and Modern Deployment of Ethernet (from Stallings, pp.385–418)

- **Switching and collision domains:** Modern Ethernet networks use **switches** (multiport bridges) instead of hubs. A switch intelligently forwards a received frame only to the port where the destination resides (based on MAC learning). As one source notes, “a layer-2 switch… provides greater performance than a hub – an incoming frame from a station is switched to the appropriate output line”. With switching, each link becomes its own collision domain. In full-duplex switched Ethernet, collisions are essentially eliminated. (In other words, switched Ethernet hubs allow dedicated full-rate channels between pairs of stations.)
    
- **Bridging and expansion:** Bridges (and later switches) let Ethernet scale beyond one segment. A bridge connects two Ethernet LANs using identical protocols (IEEE 802.3), forwarding frames between them. Bridges (and switches) improve reliability and performance by limiting contention to each segment. In practice, almost all modern LANs are built with switched Ethernet in a hierarchical star topology of switches and routers.
    
- **Higher speeds and standards:** Ethernet has evolved to higher speeds while retaining its frame and MAC format. Fast Ethernet (100BASE-TX) and Gigabit Ethernet (1000BASE-T, -X) use similar CSMA/CD protocols on twisted-pair or fiber, often in full-duplex. At Gigabit and above, switches are ubiquitous and CSMA/CD is rarely needed. (All versions of Gigabit Ethernet support only full-duplex, dropping collision rules.) Today’s Ethernet standards go up to 10 Gbps and beyond, still called Ethernet for compatibility. These runs on fiber or Cat6a/Cat7 cabling in star topologies. Vendors often use the naming “10GBASE-LR” etc for these.
    
- **Practical deployment:** Ethernet’s simplicity and flexibility have made it the dominant LAN technology. End hosts simply plug into a switch port without special configuration. VLANs (IEEE 802.1Q) allow logical segmentation on switches. Enterprises deploy Ethernet (10/100/1000 Mbps and higher) ubiquitously, using structured UTP wiring in a star and fiber backbones. The result is a scalable, reliable network architecture whose basic mechanisms (frames, MACs, CSMA/CD) are consistent with the classic Ethernet design.
    

**Sources:** Stallings, _Data and Computer Communications_ (10th ed., pp.356–419); Tanenbaum, _Computer Networks_ (4th ed., pp.304–323).

---

Originalmente, Ethernet se diseñó como un sistema **bus** basado en cable coaxial grueso (10BASE-5). Todos los nodos se conectan a un único cable compartido, de modo que cada transmisión se propaga por toda la línea y puede ser recibida por todas las estaciones.

Este diseño, sin embargo, **propicia colisiones**. Si dos estaciones transmiten al mismo tiempo, sus señales se superponen y quedan dañadas. En un bus, una estación no “sabe” que otra comenzó sino hasta que llega su señal, en estos casos, se produce un retraso de hasta 2 veces la distancia máxima entre hosts.

Con la aparición de los **hubs**, el cableado físico pasó a una topología **estrella**. Sin embargo, hay que tener en cuenta que un hub replica cualquier señal de entrada hacia todos los puertos, así que desde una perspectiva lógica, seguimos usando una topología de bus. Más adelante se explicará como los switches resuelven esto.

Queda claro que se necesita una forma de coordinar el uso de este medio para evitar conflictos y los retrasos que conllevan en la medida de lo posible

Como base histórica, Ethernet hereda ideas de **ALOHA** y **slotted ALOHA**. Ambos son protocolos de acceso aleatorio originalmente concebidos para redes de radio.

- **Pure ALOHA** permite transmitir en cualquier momento y esperar una confirmación; si no llega, se reenvía. Su utilización máxima es solo ~18% del canal debido al alto índice de colisiones .
- **Slotted ALOHA** cuantiza las transmisiones a intervalos de tiempo iguales a la longitud de trama, reduciendo solapamientos parciales y mejorando la eficiencia hasta ~37% .

El gran problema de estos protocolos es que no aprovechan el hecho de que, en las redes locales, el tiempo que tarda un paquete en llegar de un punto a otro, también conocido como **tiempo de propagación**, es mucho más corto que el tiempo que tarda "armar" estos paquetes, también conocido como **tiempo de transmisión**.

Es así como nace **CSMA** (Carrier Sense Multiple Access), el cual consiste en:

1. Escuchar el medio;
2. Si está libre, transmitir;
3. Si está ocupado, espera una cierta cantidad de tiempo

Para este protocolo, este tiempo de espera es crítico. Es así que se plantean tres enfoques a cómo responder a un canal ocupado:

- **Non-persistent:** Simplemente se espera un tiempo aleatorio antes de volver a escuchar.
- **1-persistent:** Si el canal está ocupado, se escucha hasta que finalmente quede libre, y transmitir inmediatamente.
- **p-persistent:** Este enfoque decide bajo cierta probabilidad si transmitir o esperar por un tiempo.

Cada uno de estos enfoques viene con sus propias desventajas:

- **Non-persistent:** Genera "huecos" en los que nadie usa el canal, lo que desperdicia tiempo.
- **1-persistent:** Es considerado "egoísta", ya que cada estación "pelea" por tomar control del canal, lo cual propicia colisiones.
- **p-persistent:** A pesar de ser muy inteligente, no se adapta bien a niveles de uso cambiantes.

Hasta ahora, ninguno de los protocolos mencionados permite a las estaciones detectar colisiones mientras transmiten. Estas simplemente asumen que hubo una colisión si es que no reciben la señal de acknowledgement después de cierto tiempo.

El protocolo **CSMA/CD** (con Collision Detection) propone los siguientes pasos para cada estación:

1. Si el medio está libre, transmite;
2. Si detecta una colisión mientras transmite, emite una breve señal de “jamming” para avisar a todos de lo sucedido;
3. Detiene la transmisión inmediatamente;
4. Espera un tiempo aleatorio (llamado *backoff*) antes de reintentar.

Este mecanismo reduce el tiempo “perdido” durante colisiones al mínimo posible (solo el doble de la propagación máxima) y, gracias a que este *backoff* se hace cada vez más largo con cada reintento, se mantiene una buena eficiencia tanto en cargas bajas como altas.

Aunque CSMA/CD fue clave en el Ethernet **tradicional**, su relevancia disminuye al pasar de hubs a **switches**. Los switches aíslan cada enlace en su propio dominio de colisión, y al transmitir en modo full-duplex, se eliminan las colisiones por completo. Esto lo veremos con más detalle a continuación.

Antes de pasar al siguiente punto, hay que revisar brevemente la estructura de una trama o frame. Estas tienen una estructura bien delimitada que garantiza compatibilidad y control de errores.

Comienza con el **preambulo**, una secuencia de 7 bytes alternando unos y ceros (`10101010`), seguida por el **Start Frame Delimiter** (`10101011`), el cual es simplemente un byte. Esta parte permite a las estaciones sincronizarse con precisión antes de leer los datos útiles.

Luego vienen dos campos clave: la **dirección MAC de destino** y la **dirección MAC de origen**, cada una de 6 bytes. Estas direcciones son únicas por dispositivo a nivel mundial y permiten que cada trama llegue a su destino específico. La dirección puede ser unicast (a un solo nodo), multicast (a un grupo) o broadcast (a todos).

A continuación, se encuentra el campo **Longitud/Tipo**, que puede indicar o bien el tamaño del campo de datos o el tipo de protocolo de nivel superior (como IP o ARP).

Viene ahora el más importante de todos: el campo que contiene los datos a transmitir. Este puede tener entre 46 y 1500 bytes, y si los datos reales son más cortos, se rellena con ceros para alcanzar el mínimo.

Finalmente, tenemos al Frame Check Sequence, el cual es un código de 4 bits que permite detectar errores durante la transmisión. Si el receptor encuentra una discrepancia, simplemente descarta la trama.

Esta estructura, sencilla pero robusta, ha sido una de las razones del éxito y longevidad de Ethernet como estándar.
