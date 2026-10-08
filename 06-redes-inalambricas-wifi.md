# Semana 6: Redes Inalámbricas

## Salto de frecuencia

Las señales de salto de frecuencia hacen que la señal salte y no se pueda controlar fácilmente desde afuera: si estás en la misma frecuencia puedes "controlar" algo (ej. una bomba teledirigida), pero si la señal va saltando de frecuencia ya no puedes.

## Historia del WiFi

- En 1980 las computadoras se conectaban a internet con **Ethernet** (cable).
- Luego se quiso comunicarlas por señal de radio.
- Se aplicaron las **transformadas rápidas de Fourier** junto con señales de radio, y de ahí nació el WiFi.
- El estándar **802.11** es el que se conocería como "WiFi".

## Cómo funciona

- Se transmite mediante **ondas de radio**, medidas en **gigahercios** (2.4 GHz o 5 GHz).
  - **2.4 GHz** → distancias largas.
  - **5 GHz** → distancias cortas.
- El código binario se transforma en onda (en WiFi), se vuelve paquetes pequeños y se envía mediante enrutadores/access points.
- El WiFi trabaja dentro del **espectro electromagnético**.

## Salud

Las ondas de radio del WiFi son de **baja potencia** o **no ionizantes**: no hay evidencia de que hagan daño a la salud humana.

## Access Point

- Un access point se conecta a varios equipos a la vez (hasta un celular se vuelve uno más conectado).
- Un access point con varias antenas irradia mejor la señal.
- **Antena omnidireccional:** cubre todas las direcciones.
- **Antena direccional:** se usa para enlaces punto a punto (1 a 1).

802.11 trabaja en **Capa 2**.

### Proceso de conexión

```
1° Se descubre el AP (access point) inalámbrico.
2° Te conectas mediante la contraseña.
3° Te asocias al access point.
```

## Hub vs Switch

- El **hub** es el "abuelo" del switch.
- El hub usa un **medio compartido**: envías un paquete y lo manda a todos (similar al broadcast). Solo envía o recibe, no ambos (half-duplex).
- El **switch** sí puede enviar y recibir al mismo tiempo (full-duplex).
- El **aire** es el medio físico por donde viaja el WiFi.

## CSMA/CA (evita colisiones)

```
1° La PC primero escucha si alguien está irradiando/enviando señal al access point.
2° Si no escucha a nadie (no hay ruido), avisa al access point: RTS (Request To Send).
3° El access point responde que está libre: CTS (Clear To Send).
```

- Campo de **duración**: espera a que el que está transmitiendo termine, antes de enviar.
- Si dos computadoras quieren enviar al mismo tiempo ocurre una **colisión**, y ambas deben esperar un tiempo antes de volver a intentar.
- Si no hay nadie transmitiendo, se activa el CTS y se da el turno para enviar.

> **CSMA/CD** evita colisiones en redes cableadas. En redes full-duplex los datos se envían y reciben al mismo tiempo sin competir por el medio. Las conexiones inalámbricas también deben evitar colisiones, pero como no hay cable, revisan los **canales** y envían los datos solo si no hay nadie usándolos (CSMA/CA).

## Canales

Selección de canal: del **1 al 14** en la banda de 2.4 GHz.

## Seguridad de redes

- Ocultar el **SSID**.
- Filtrar por **dirección MAC**.

> El hub es poco eficiente porque todos los puertos comparten el mismo medio físico.

## Configuración en Packet Tracer

Para configurar la seguridad inalámbrica de un Access Point:

```
1. Entrar al Access Point en Packet Tracer.
2. Cambiar el valor por defecto a WEP.
3. Configurar la Key: 10 dígitos hexadecimales.
```

Para que una laptop/PC se conecte:

```
1. La laptop necesita una NIC inalámbrica (ej. módulo WP300N).
2. En el equipo (Desktop), entrar a "PC Wireless".
3. Buscar la red (SSID) y colocar la contraseña (key WEP).
```
