# Outbound, IPv4, Máscaras y Subneteo

Outbound da información, flujo hacia abajo, capa 1 aplicación, depende del modelo.

Segmento, paquete, trama.

## IPv4 básico

IPv4 son 32 bits.

```
1 bit  -> 0 y 1
2 bits -> 4 valores
3 bits -> 8 valores
...
12 bits -> 4096 valores
```

Dirección IP: son 4 grupos de 8 bits (32 bits), cada grupo puede ser de máx 255 (2 a la 8, -1).

## Máscara

Máscara e IP ambos de 32 bits, pero la máscara es subred. Su diferencia es que la máscara es una cadena de unos, que en algún momento en la máscara habrá un 0 y se completa los 32 con ceros.

```
1111 1111 -> 255
```

- Si hay en la máscara **255** → representa a la **red** en la IP.
- Si hay **0000** en la máscara → hay esa cantidad de **host** que lo representa.

```
255.255.255.00000000
24 bits de RED, 8 de host
```

Cantidad de 0 → cantidad de bits del host.

## AND lógico (Y lógico)

Para Y (lógico): multiplicación.

```
01 -> 0
00 -> 0
10 -> 0
11 -> 1
```

## ID de red

Une IPv4 y máscara: si en la máscara hay 0, lo vuelve 0.

- Primer valor: cuando los bits de host son 0, no le puedes dar porque no es útil.
- Si fueran todos 1, tampoco lo puedes dar porque es broadcast (no quieres comunicarte contigo mismo).

Redes útiles → 2 a la (# bits host) → 254 IP útiles para host.

IP host 0 → `0000 0000`. Puedes usar todas menos `0000 0000` y `1111 1111` (interconectas).

La primera red útil se le da a la conexión de router (interfaz del router).

### Ejemplo

```
IPV4:    192.168.255.10
MASCARA: 255.255.255.00000000 (11111111.11111111.11111111.00000000)

RED: 192.168.255.0 (es 0 porque según Y lógico se vuelve 0)
```

Toda red comparte la máscara.

```
MASCARA: 255.255.255.00000000  -> formato largo
MASCARA: /24                   -> formato corto (24 unos y 8 ceros)
```

Si tiene 11 ceros = 11 bits de host.

Siempre grupos de 4, bits de 8 (32 bits siempre).

### Ejercicio: ID de red de 10.25.140.200 /26

```
IP:      10.25.140.200 -> 200 en binario: 11001000
MASCARA: 255.255.255.11000000

ID RED (Y lógico dígito por dígito): 10.25.140.192
```

- Redes útiles: 2 a la 6, -2 → **62**
- 1ª IP útil se la da al router siendo su **default gateway**, porque el router comunica por defecto de manera externa.

| nombre | ID RED | /N | máscara | 1ª IP útil | última IP útil | IP broadcast |
|---|---|---|---|---|---|---|
| A | 10.25.140.192 | /26 | 255.255.255.192 | 10.25.140.193 | 10.25.140.254 | 10.25.140.255 |

```
ID IP + 1 = 1° RED ÚTIL
IP útiles/host = 2^(cantidad de "0") - 2
```

- **Switch** → lo comunica entre ellos en la misma red.
- 1ª IP útil es default gateway, para que el router se comunique al exterior.
- Subnetear: parte varias redes, ej. una /16 a una /24.
- Interfaz de router: dominio de broadcast. Por cada red distinta, una interfaz de router distinta.

### Ejercicio: 10.20.30.15

```
IPV4:    10.20.30.15 -> 10.20.00011110.00001111
MASCARA: 255.255.11000000.00000000

ID RED: 10.20.0.0/18

primera red útil: 10.20.0.1 -> (10.20.0.0 no se toca)
última red útil:  10.20.11000000.00000000 -> 10.20.63.254 -> broadcast: .255
```

> **La red nunca se toca.**

### Ejercicio: 192.168.10.0/24 → /26

```
192.168.10. 0000 0000
192.168.10. 0100 0000
192.168.10. 1000 0000
192.168.10. 1100 0000
```

| Red | ID | /N | Máscara | 1ª útil | última útil | broadcast |
|---|---|---|---|---|---|---|
| RED1 | 192.168.10.0 | /26 | 255.255.255.0 | 192.168.10.1 | 192.168.10.62 | 192.168.10.63 |
| RED2 | 192.168.10.64 | /26 | 255.255.255.0 | 192.168.10.65 | 192.168.10.126 | 192.168.10.127 |
| RED3 | 192.168.10.128 | /26 | 255.255.255.0 | 192.168.10.129 | 192.168.10.190 | 192.168.10.191 |
| RED4 | 192.168.10.192 | /26 | 255.255.255.0 | 192.168.10.193 | 192.168.10.254 | 192.168.10.255 |

```
¿Cuántos host? 2^N - 2
¿Cuántos bits de host? N
```

### Problema 2: 172.16.0.0/22, 10 bits de host

La red más grande tiene 40 host.

```
Qué valor se acerca más a esos bits (2^6 - 2) >= 40
Tengo 10 bits, quiero 6 bits
Divido con 10 - 6 = 4 bits de host
```

El problema pide las 5 primeras redes.

> La red no se toca.

```
172.16.00000000.00000000
172.16.00000000.01000000
172.16.00000000.10000000
172.16.00000000.11000000
172.16.00000001.00000000
```

```
172.16.0.0
172.16.0.64
172.16.0.128
172.16.0.192
172.16.1.0
```

```
172.16.00000001.01000000
172.16.00000001.10000000
172.16.00000001.11000000
172.16.00000010.00000000
172.16.00000010.01000000
172.16.00000010.10000000
172.16.00000010.11000000
172.16.00000011.00000000
172.16.00000011.01000000
172.16.00000011.10000000
172.16.00000011.11000000
```

### Ejercicio: 172.23.69.0/24

Hay 8 bits host, el host más grande es 30.

```
Tengo 8 bits, quiero 5 bits (2^5 = 32 - 2)
Divido con 3 bits de host (hay 2^3 redes)
```

Pide 4 redes.

> La red no se toca.

```
172.23.69.00000000
172.23.69.00100000
172.23.69.01000000
172.23.69.01100000
172.23.69.10000000
172.23.69.10100000
172.23.69.11000000
172.23.69.11100000
```

| Área | ID Red | Máscara | 1ª IP útil |
|---|---|---|---|
| MARKETING | 172.23.69.0/24 | 255.255.255.0 | 172.23.69.1 |
| INGENIERIA | 172.23.69.32/24 | 255.255.255.0 | 172.23.69.33 |
| VENTAS | 172.23.69.64/24 | 255.255.255.0 | 172.23.69.65 |
| LOGISTICA | 172.23.69.96/24 | 255.255.255.0 | 172.23.69.97 |
| INTERFAZ | 172.23.69.128/24 | 255.255.255.0 | 172.23.69.129 |
| GENERICO1 | 172.23.69.160/24 | 255.255.255.0 | 172.23.69.161 |
| GENERICO2 | 172.23.69.192/24 | 255.255.255.0 | 172.23.69.193 |
| GENERICO3 | 172.23.69.224/24 | 255.255.255.0 | 172.23.69.225 |

---
> 💡 **Notita:** El truco rápido para el "salto" entre redes en subneteo es `256 - (último octeto de la máscara)`. Por ejemplo, con /26 (máscara .192), el salto es `256 - 192 = 64` → por eso las redes van de 64 en 64 (.0, .64, .128, .192). Te ahorra escribir todo el binario cuando ya tienes práctica.
