# BITACORA DE COMANDOS CISCO PACKET TRACER

##### MOLLINEDO SILES RENZO SEBASTIAN

# Configuración General
# SWITCH

## Entrar en modo privilegiado:

**Utilizar el comando enable:**

```bash
Switch> enable
Swtich#
```
---
## Ver la configuración actual del switch:

**Utilizar el comando show running-config**
```bash
Switch> show running-config
```` 
---

## Poner un nombre al switch:

>Ejecutar el comandos `configure terminal`, una vez dentro del módulo de configuración ingresar el comando hostname seguido del nombre deseado.

```bash
Switch# configure terminal
Switch(config)# hostname SW
S1(config)# exit
S1>
```
---
## Configurar mensaje del día MOTD (Message of the day):

```bash
S1> enable
S1# configure terminal
S1(config)# banner motd "Message of the day"
S1(config)# exit
S1#
```
---

## Configurar una contraseña cifrada para proporcionar acceso seguro al modo privilegiado


**Ingresar `configure terminal` habilitar el comando secret junto con la contraseña.**

```bash
S1> enable
S1# configure terminal
S1(config)# enable secret itsasecret
S1(config)# exit
S1#
```
---

## Creación de Usuarios en Switches Cisco
```bash
Switch(config)#username <nombre_usuario> privilege <nivel> secret <contraseña>
```

## Guardar los cambios de la configuración en la NVRAM:
```bash
S1> enable
S1# copy running-configuration starup-configuration
```
---

# ROUTER

## Asignar direcciones IP a interfaces:

```bash
R1> enable
R1# configure terminal
R1(config)# interface GigabitEthernet0/0 
R1(config-if)#ip address 172.31.1.1 255.255.255.240
R1(config-if)#no shutdown
```

## Interfaz serial:

```bash
R2(config)#interface Serial0/0/0
R2(config-if)#ip address 172.31.1.78 255.255.255.240
R2(config-if)#no shutdown
```
---
## Habilitar Telnet:

```bash
Router(config)# line vty 0 4
Router(config-line)# login
Router(config-line)# password p4ssw0rd
Router(config-line)# exec-timeout 
Router(config-line)# exit
```
---
## Configurar IPv6 en un router:
```bash
R1(config)# ipv6 unicast-routing
R1(config)#interface gigabitEthernet 0/0
R1(config-if)#ipv6 address 2001:DB8:ACAD:A::1/64
R1(config-if)#ipv6 address FE80::1 link-local
R1(config-if)#no shutdown
R1(config-if)#exit
```
---
# SWITCHING

## Configuración básica de un switch con usuarios y contraseña

```bash
Switch(config)#hostname D1
D1(config)#enable secret privilegiado
D1(config)#username admin privilege 15 secret admin15
D1(config)#username tecnico privilege 0 secret tecnico15
```
---

## Configuración de interfaces

```bash
D1(config)#interface range FastEthernet0/1 - 5
D1(config-if-range)#duplex half
D1(config-if-range)#speed 10
D1(config-if-range)#exit

D1(config)#interface range FastEthernet0/6 - 10
D1(config-if-range)#duplex full
D1(config-if-range)#speed 100
D1(config-if-range)#exit

D1(config)#interface range FastEthernet0/11 - 24
D1(config-if-range)#shutdown
D1(config-if-range)#exit
```
---

## Configuración de VLAN para administración

```bash
D1(config)#interface Vlan1
D1(config-if)#ip address 192.168.100.2 255.255.255.0
D1(config-if)#no shutdown
D1(config-if)#exit
```
---

## Configuración de puerta de enlace predeterminada

```bash
D1(config)#ip default-gateway 192.168.100.1
```
---

## Configuración de acceso remoto (líneas VTY)

```bash
D1(config)#line vty 0 2
D1(config-line)#login local
D1(config-line)#exit
```
---

## Finalizar configuración

```bash
D1(config)#end
D1#
```

# SWITCH – Comandos de Configuración y Referencia

## Configuración de puerta de enlace predeterminada

```bash
Switch(config)#ip default-gateway <IP_DE_GATEWAY>
Switch#show ip interface brief
```
---

## Configuración de Interfaces del Switch

```bash
Switch(config)#interface fa0/0
Switch(config-if)#switchport mode access
Switch(config-if)#spanning-tree portfast
```

> El comando `spanning-tree portfast` deshabilita el protocolo STP en puertos de acceso. Es útil en enlaces hacia hosts, **no debe usarse en enlaces troncales entre switches**.

```bash
Switch(config-if)#duplex [half | full | auto]
Switch(config-if)#speed [10 | 100 | auto]
```

---

## Visualizar Tabla de Direcciones MAC

```bash
Switch#show mac-address-table
```

---

## Asignar Dirección MAC Estática

```bash
Switch(config)#mac address-table static <DIRECCION_MAC> vlan 1 interface fastEthernet 0/12
```

---

# SWITCH CAPA 3 (Layer 3 Switch)

>Los switches de capa 3 (L3) son compatibles con todos los comandos de switches de capa 2 (L2), **con algunas extensiones adicionales**.

---

## Interfaces Virtuales (SVI)

> **SVI** (Switch Virtual Interface) permite asignar direcciones IP al switch.  
> En switches L3, **cada SVI actúa como gateway para su VLAN**, reemplazando al router.

---
## Crear una VLAN

```bash
Switch(config)#vlan <ID_VLAN>
Switch(config-vlan)#name <NOMBRE>
Switch(config-vlan)#exit
```
---
## Comandos Exclusivos de Switch Layer 3

```bash
Switch(config)#ip routing
```

Habilita la función de enrutamiento entre VLANs.

```bash
Switch(config)#interface fa0/1
Switch(config-if)#no switchport
```

> El comando `no switchport` convierte una interfaz de capa 2 en una interfaz de capa 3 (ruteable).
---
