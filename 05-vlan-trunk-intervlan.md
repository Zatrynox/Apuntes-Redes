# Semana 5: VLAN, Trunk e InterVLAN

[Ejercicio 2026-2 router on stick v0.pkt](https://aulavirtual.upc.edu.pe/bbcswebdav/internal/courses/1ASI0640-2620-7632/messages/_1464234_1/embedded/ejercicio%202026-2%20router%20on%20stick%20v0.pkt)

## Protocolo ARP

Para encontrar MAC address de computadora destino, para hacer broadcast ARP, hace info a su IP hacia MAC address destino e inicio.

## CLI del switch

Al dar enter usas `show` y demás, pero está limitado.

Nivel superior al usar `enable`: aparece el `#`, y puedo ver datos de interfaces.

```
show interfaces fa0/1
```

`configure terminal` si lo escribe configure en un mayor nivel.

Poner `interface fa0/3` hace que puedas cambiarla.

`exit` sales, y no sales al nivel anterior.

## VLAN = ID RED

Se divide en redes para que la info sea solo entre las redes o entre las mismas VLANs, que son para los switches.

VLANs solo se comunican entre ellas.

```
show vlan brief
```
Para ver todas las VLANs.

## Crear VLANs

Para crear VLANs es del 2 al mil.

```
1. configure terminal
2. vlan n          (n siendo el número que crees)
3. name m           (m siendo el nombre de ese VLAN)
4. end
```

> Tienes que crear VLAN para cada switch. Se puede editar el nombre luego de creado.

## Puertos para las VLANs

```
Puerto(PC)              -> access
Puerto(switch o router) -> trunk
```

Trunk no asignadas a una VLAN.

### Asignar puertos a VLAN (access)

```
1. configure terminal
2. interface fa0/x        (x siendo la conexión de puerto access, no existe para trunk)
3. switchport mode access
4. switchport access vlan y   (y siendo los ya creados)
5. end
```

## Trunk o troncal (para ambos)

Con un solo puerto pasan varias VLANs. `G0/1` o `G0/2` son trunk.

```
0. configure terminal
1. identifica el puerto modo trunk, interface fa0/x   (x que se usó como trunk)
2. switchport mode trunk
3. switchport trunk allowed vlan all
4. end
```

Para ver el trunk:

```
show interface f0/1 switchport
```

## Pasos del profe

1. Crear todas las VLANs en TODOS los switches.
2. Asignar los puertos access a las VLANs en todos los switches.
3. Asignar los puertos trunk a las VLANs en todos los switches.

Método para no gastar muchos puertos en el router → **router on stick**.

### 4. InterVLAN

```
ROUTER ON STICK  -> para proyecto provincias
SW L3            -> para lo de Lima
```

## Protocolo dot1Q — Router on a Stick

1. Enciendes el puerto que conecta el router con el switch, sea manual o en terminal:
   ```
   configure terminal
   interface fa0/0
   no shutdown
   ```
2. Haces en el router `interface fa0/x.m` (x siendo lo que conecta al switch con el router, y m siendo una subdivisión de la red, para que todos salgan de un solo puerto y no se sature).
3. Pones `encapsulation dot1Q y` (siendo y la VLAN creada).
4. Pones gateway y máscara:
   ```
   ip address AAA.AAA.AAA.AAA BBB.BBB.BBB.BBB
   ```
5. `exit` (se hace para todos los VLANs).

> Quitar de filtros CDP, DTP y STP, en Cisco.

## Método de Switch de Capa 3 (SVI)

```
Switch_D1(config)#interface Vlan y
Switch_D1(config-if)#ip address 192.168.10.1 255.255.255.0
Switch_D1(config-if)#no shutdown
Switch_D1(config-if)#exit

Switch_D1(config)#interface Vlan y
Switch_D1(config-if)#ip address 192.168.20.1 255.255.255.0
Switch_D1(config-if)#no shutdown
Switch_D1(config-if)#exit

Switch_D1(config)#ip routing
```
