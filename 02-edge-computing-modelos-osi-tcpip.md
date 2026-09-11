# Edge Computing, Modelos OSI/TCP-IP y Protocolos

Edge computing: un modelo nos dice cómo se debe trabajar eso o dirigirse.

## Modelos

Modelos: **OSI** o **TCP/IP**.

- TCP/IP → modelo simple.
- Los modelos definen estructuras y diferentes categorías.

**WIFI MODELO** → 802.11

TCP/IP dice que debe haber una computadora **source** (origen) a una computadora **destino**.

También debe haber un canal de medio (como el wifi).

**NIC**: punto que permite conectar a una red (Network Interface Card).

## Protocolos

Protocolos → dicen que debes hacer:

- Deben haber un emisor y receptor identificados.
- Idioma y gramática común.
- Velocidad y momento de entrega (deben saber y trabajar a la misma velocidad).
- Confirmación de acuse de recibo (confirmar que se recibió la información).

Los protocolos de red definen reglas por software, hardware o ambos.

Dan seguridad, permiten comunicación entre muchas redes, dan información de la red entre muchos caminos para buscar mejor ruta. Detección de servicios es para detectar algunos dispositivos conversando entre routers, testeando cuál está menos saturado.

### Función de protocolos

- **Direccionamiento** → solo un emisor y un receptor.
- **Confianza**
- **Control de flujo** → garantizar flujo de datos a una velocidad eficiente.
- **Secuenciación** → etiqueta cada segmento de datos.
- **Detección de errores** → determinan los datos dañados.
- **Interfaz de la app** → comunicaciones entre aplicaciones red.

### Protocolos informáticos

Origen codifica el mensaje, envía el mensaje y lo decodifica.

Los formatos de los mensajes dependen del tipo de mensaje y el canal que se utilice para entregar el mensaje.

Encapsulamiento del mensaje: ya está definido el IP de mi máquina y a dónde va al destino. Cada cosa que haces en la red mandas tu IP para mandar una consulta a internet.

- **IP** → dirección única.
- El **protocolo** define el tamaño del mensaje.

### Tipos de comunicación

- Cuando una computadora se comunica con otra computadora de su red → **unicast** (unidifusión).
- Cuando la compu se conecta con más de una → **multicast** (multidifusión).
- Si una computadora se comunica con todos menos con él mismo → **broadcast** (difusión).

## Proceso por capas (layers)

Computadora origen manda un mensaje. Esta tiene que pasar todos los protocolos de cada capa, lo envía a la siguiente capa "hace algo", y lo envía a la red.

En la red, hacia la compu destino, procesa lo que hace él siguiendo a su equivalente; en la segunda capa (por así decirlo) llega el último mensaje a ese grupo comparando al lado origen.

## Modelo OSI y Modelo TCP/IP

**Outbound**: el mensaje baja de capa en capa.

- La capa 7 tiene datos.
- Comienza en la capa **Aplicación**, y la capa 4 (**Transporte**) divide la información que se quería enviar, con un header de información de cómo armarlo, y luego lo encapsula. El PDU en esa capa es **segmento** (info dividida).
- La capa 3 (**Red**) también agrega su propio header y de nuevo lo encapsula; esa pequeña unidad se llama **paquete**.
- En la capa 2 se llama **trama**.
- En la capa 1 se vuelve **bits** ("código binario").

**Inbound**: el mensaje sube de capa para decodificar el mensaje.

- En la capa 2 de esta parte, desencapsula la trama.
- En la capa 3, desencapsula el paquete.
- En la capa 4, desencapsula el segmento.
- Y sube la data hasta la capa 7.

La capa 7 es la más cercana al usuario; la capa 8 es el usuario (diferencia de nombres entre TCP/IP y OSI).

El modelo en capas ayuda porque a diferentes modelos les sirve las capas superiores.

Capa con protocolo **IPv4** → capa de internet (TCP/IP). Recuerda la forma y estructura de ambos, y aparte lo que tiene de protocolos en cada capa.

> RECORDAR DÓNDE SE UBICA CADA PROTOCOLO - INGLÉS Y ESPAÑOL

Comunicación ida y vuelta:

- **Router** maneja 3 capas (capa 3): comunicación por capas, direccionamiento y segmentación y reensamble.
- **Switch** maneja 2 capas (capa 2).
- Capa **física** (capa 1): todo lo tocable.

En la trama: los 3 headers acumulados.

> SELECCIONAR Y APLASTAR LA NUBE PARA AGRUPARLOS EN CLUSTER

---
> 💡 **Notita:** Para no confundir el orden de encapsulamiento, puedes pensarlo así: **Datos → Segmento (Cap.4) → Paquete (Cap.3) → Trama (Cap.2) → Bits (Cap.1)**. Es la misma secuencia que ya tienes, solo que en outbound vas "hacia abajo" agregando headers, y en inbound vas "hacia arriba" quitándolos (desencapsulando) en el orden inverso.
