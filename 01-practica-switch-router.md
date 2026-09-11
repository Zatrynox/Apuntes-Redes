# Práctica: Switch, Router y NIC

**NÚMERO DEL PROFE:** 999 790 226

## Conceptos base

- Host se conecta a un network para llegar a otro dispositivo.
- **NIC** (Network Interface Card): tarjeta que te da acceso a la red para tener conectividad con otro dispositivo final.
- En la red o network tenemos: **Switch (Layer 2)**.

Dispositivo inicial, inicia la comunicación pasando por la red hacia dispositivo final, la cual es donde finaliza la comunicación. La NIC permite que tu dispositivo se conecte al network o red.

NIC es el puerto físico / interfaz para la conexión a una red.

## Cableado

- 🔶 **Rayo naranja** → elige automáticamente.
- Cable de (PC o laptop) a Switch = cobre fuerte directo.
- Cable de Switch al Router = cobre fuerte directo.
- **HWIC 2T** → ayuda a poner el puerto serial a los router.

De PC a Switch se enciende normal. La cosa es de Router a Switch.

## Activar puertos

Cuando pasas el mouse por lo rojo, sale los puertos que debes prender. Das doble click a cada uno y lo activas en la pestaña **INTERFACE** de config.

## Configuración de IP

- Cambias IP en computadora o laptop: pestaña **Desktop** y pones todo lo que se pide.
- En el router: **config → interface** según lo que te pidan.

## Miscelánea

En **Miscellaneous → Edit Filters**, lo que quitas es: **CDP, DTP y STP**.

## Orden de los apuntes

- Este md (práctica switch/router) es el **1°**.
- El que empieza con "edge computing" es el **2°**.
- El que empieza con "outbound" es el **3°**.

---
> 💡 **Notita:** CDP, DTP y STP son protocolos de Cisco/switching que normalmente se filtran en Packet Tracer para que la captura de tráfico (por ejemplo con Wireshark) no se llene de "ruido" de administración de la red y puedas ver solo el tráfico que te interesa.
