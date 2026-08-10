# 0104 Â· MÃ³dulo 4: Redes â€” Fundamentos

> Curso 01 Â· MÃ³dulo 4 de 6 Â· Temas: componentes de red, el modelo TCP/IP en 5 capas, IP, DNS, DHCP

---

## Objetivos de este mÃ³dulo

- [ ] Identificar los componentes de una red (hosts, NIC, router, switch)
- [ ] Explicar el modelo TCP/IP de 5 capas con un ejemplo real
- [ ] Entender quÃ© son IPv4, MAC, DNS y DHCP
- [ ] Ejecutar comandos bÃ¡sicos de diagnÃ³stico de red
- [ ] Diferenciar LAN, WAN y Internet

---

## 1. Componentes bÃ¡sicos de una red

| Componente | FunciÃ³n |
|------------|---------|
| **Host / dispositivo final** | PC, celular, impresora (lo que usa la red) |
| **NIC (tarjeta de red)** | Hardware que conecta el equipo a la red |
| **Switch** | Conecta mÃºltiples dispositivos en la misma red local |
| **Router** | Une redes distintas y da salida a Internet |
| **Cableado / Wi-Fi** | El medio fÃ­sico |
| **Servidor** | Proporciona servicios (web, correo, archivos) |

```mermaid
flowchart LR
    PC1[PC 1] --> SW[Switch]
    PC2[PC 2] --> SW
    IMP[Impresora] --> SW
    SW --> R[Router]\nSalida a Internet
```

---

## 2. El modelo TCP/IP de 5 capas

Es el mapa mental que usa el soporte profesional (la versiÃ³n prÃ¡ctica del modelo OSI de 7 capas).

```mermaid
flowchart TB
    A[Capa 5 - Aplicacion\nHTTP, DNS, SMTP - datos visibles para el usuario] --> B[Capa 4 - Transporte\nTCP/UDP - puertos y confiabilidad]
    B --> C[Capa 3 - Red\nIP - direcciones y rutas entre redes]
    C --> D[Capa 2 - Enlace de datos\nEthernet/Wi-Fi - MAC y tramas locales]
    D --> E[Capa 1 - Fisica\nSeÃ±ales, cables, ondas]
```

![Modelo TCP/IP de 5 capas](./diagramas/tcpip-5-capas.svg)

**Ejemplo cotidiano** (envÃ­as un mensaje de WhatsApp):

1. **FÃ­sica**: la seÃ±al Wi-Fi del celular hacia el router.
2. **Enlace**: tu Wi-Fi empaqueta la trama con las MAC.
3. **Red**: el IP del mensaje viaja de tu red al servidor de WhatsApp (rutas).
4. **Transporte**: TCP garantiza que llegue completo (nÃºmeros de secuencia).
5. **AplicaciÃ³n**: WhatsApp (protocolo de mensajerÃ­a) lo muestra.

---

## 3. Vocabulario imprescindible

### DirecciÃ³n IP (IPv4)
Identificador de 32 bits escrito en 4 octetos: `192.168.1.50`.
- Define **red** y **host** con la mÃ¡scara (`/24` = 255.255.255.0).
- Rango privado tÃ­pico del hogar: **192.168.x.x** â€” **10.x.x.x** â€” **172.16â€“31.x.x** (no salen a Internet).
- **IPv6**: el reemplazo (128 bits, 8 grupos hexadecimales) que resuelve la escasez de IPv4.

### DirecciÃ³n MAC
Identificador fÃ­sico Ãºnico de 48 bits de cada tarjeta de red (los primeros 3 bytes = fabricante).
Ejemplo: `3C:7C:3F:AB:CD:EF`. Funciona **en la red local** (capa 2).

### DNS (Sistema de Nombres de Dominio)
Convierte `www.google.com` â†’ `142.250.190.46` (traducciÃ³n de nombres a IPs).
Sin DNS, tendrÃ­amos que memorizar nÃºmeros.

### DHCP (AsignaciÃ³n dinÃ¡mica de IP)
El router **entrega** automÃ¡ticamente IP, mÃ¡scara, gateway y DNS a cada equipo que se conecta â€” proceso DORA (Discover â†’ Offer â†’ Request â†’ Acknowledge).

### Gateway (puerta de enlace)
La direcciÃ³n del router en tu red (normalmente `x.x.x.1`) â€” la salida hacia otras redes.

---

## 4. LAN vs WAN vs Internet

| Tipo | Alcance | Ejemplo |
|------|---------|---------|
| **LAN** | Red local (un edificio/oficina) | La red de tu casa u oficina |
| **WAN** | Red que une redes locales (ciudad/paÃ­s/mundo) | La red de sucursales de una empresa |
| **Internet** | La WAN mÃ¡s grande del mundo | Todo interconectado |

---

## 5. DiagnÃ³stico bÃ¡sico (primeros 4 comandos del TÃ©cnico)

```powershell
# 1) Â¿Tengo IP?
ipconfig /all

# 2) Â¿Llego al router?
ping 192.168.1.1

# 3) Â¿Llego a Internet?
ping 8.8.8.8

# 4) Â¿Se resuelven nombres?
nslookup google.com
```

**Regla de oro**: si el ping al router funciona pero no al 8.8.8.8 â†’ el problema es Internet/proveedor. Si ni el router responde â†’ problema de red local o Wi-Fi.

> **Dato Ãºtil**: una IP que empieza con **169.254.x.x** (APIPA) significa que el DHCP no respondiÃ³ y el equipo se autoconfigurÃ³ â€” casi siempre es cable/red caÃ­da.

---

## PrÃ¡ctica del mÃ³dulo

1. Ejecuta los 4 comandos de diagnÃ³stico en tu PC y anota resultados.
2. Identifica en tu casa: router, switch (si hay), MAC de tu celular (Ajustes â†’ Acerca del telÃ©fono).
3. Cambia el DNS de tu PC a `1.1.1.1` (Cloudflare) o `8.8.8.8` (Google) y compara tiempos de resoluciÃ³n.
4. Observa con `netstat` (`netstat -n`) las conexiones activas de tu equipo.

## Plataformas gratuitas para practicar

- **Cisco Networking Academy** (https://www.netacad.com): *Networking Basics* â€” el curso gratuito que sigue este temario + **Packet Tracer** para armar redes visualmente.
- **subnettingpractice.com**: entrena subredes.
- **Wireshark** (https://www.wireshark.org): captura tu propio trÃ¡fico y mira las 5 capas "en vivo".

---

## Checklist de dominio â€” MÃ³dulo 4

- [ ] Explico IP vs MAC con un ejemplo (casa vs nombre de la persona)
- [ ] Describo el viaje de un dato por las 5 capas
- [ ] Conozco LAN/WAN/Internet y quÃ© es el gateway
- [ ] Diagnostico conectividad con ipconfig/ping/nslookup
- [ ] Identifico una IP APIPA y quÃ© significa
- [ ] He usado Packet Tracer o Wireshark al menos una vez

