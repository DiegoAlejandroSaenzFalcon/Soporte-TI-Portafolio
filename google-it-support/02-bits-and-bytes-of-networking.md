# Manual Técnico de Redes: Bits y Bytes de las Redes de Computadoras

> **Curso 2 — Especialización de Soporte TI de Google**
> **Nivel**: Ingeniería de Soporte

---

## 1. El Modelo de 5 Capas (TCP/IP)
A diferencia del modelo OSI de 7 capas, en el soporte práctico nos enfocamos en el modelo TCP/IP:

| Capa | Nombre | Función Principal | Protocolos/Hardware |
| :--- | :--- | :--- | :--- |
| **5** | **Aplicación** | Donde residen las apps (Navegador, Email). | HTTP, SMTP, DNS, FTP |
| **4** | **Transporte** | Comunicación extremo a extremo y puertos. | TCP, UDP |
| **3** | **Red** | Direccionamiento global y rutas. | IP (IPv4, IPv6), ICMP |
| **2** | **Enlace de Datos** | Transferencia local (entre vecinos). | Ethernet, Wi-Fi, Switches, MAC |
| **1** | **Física** | El medio físico (cables, ondas). | Cables UTP, Fibra, Señales Eléctricas |

---

## 2. Capa Física y de Enlace (El Cimiento)
### 2.1 Direcciones MAC (Media Access Control)
*   Identificador único de 48 bits para cada tarjeta de red (NIC).
*   **OUI (Organizationally Unique Identifier)**: Los primeros 3 octetos identifican al fabricante (ej. Apple, Intel).
*   **Unicast vs Multicast vs Broadcast**: Cómo se envía la información (a uno, a varios o a todos en la red local).

### 2.2 Hubs vs Switches
*   **Hub**: Dispositivo "tonto" (Capa 1) que repite el tráfico a todos los puertos (genera colisiones).
*   **Switch**: Dispositivo inteligente (Capa 2) que lee las MACs y envía los datos solo al puerto correcto (usa una tabla CAM).

---

## 3. Capa de Red (El Direccionamiento)
### 3.1 Protocolo IP (IPv4)
*   Estructura: 4 octetos (32 bits). Ejemplo: `192.168.20.153`.
*   **Máscara de Subred**: Define qué parte es la red y qué parte es el host (ej. `/24` o `255.255.255.0`).
*   **CIDR (Classless Inter-Domain Routing)**: Método moderno para asignar IPs sin las rígidas clases A, B, C.

### 3.2 Enrutamiento (Routers)
*   El router conecta redes distintas.
*   **Puerta de Enlace (Gateway)**: La salida de tu red local hacia el mundo (generalmente la `.1` de tu red).

---

## 4. Capa de Transporte (TCP vs UDP)
### 4.1 TCP (Transmission Control Protocol)
*   **Confiable**: Garantiza que los datos lleguen completos y en orden.
*   **Three-Way Handshake**:
    1.  SYN (¿Podemos hablar?)
    2.  SYN-ACK (Sí, yo también quiero)
    3.  ACK (¡Listo, allá van los datos!)

### 4.2 UDP (User Datagram Protocol)
*   **Rápido**: No espera confirmación. Se usa para video en vivo, llamadas de voz y juegos online donde la velocidad es prioridad sobre la perfección.

---

## 5. Servicios Esenciales: DNS y DHCP
### 5.1 DHCP (Asignación Automática)
Proceso **DORA**:
1.  **D**iscover: El cliente busca un servidor DHCP.
2.  **O**ffer: El servidor ofrece una IP.
3.  **R**equest: El cliente pide usar esa IP.
4.  **A**cknowledge: El servidor confirma.

### 5.2 DNS (Resolución de Nombres)
*   **Zonas de Búsqueda**: Directa (Nombre -> IP) e Inversa (IP -> Nombre).
*   **Tipos de Registro**:
    *   `A`: IPv4.
    *   `AAAA`: IPv6.
    *   `MX`: Servidores de correo.
    *   `CNAME`: Alias.

---

## 6. Resolución de Problemas de Red (Troubleshooting)
1.  **¿Es físico?** Revisar cables y luces de enlace.
2.  **¿Tengo IP?** `ipconfig` (Windows) o `ip a` (Linux). Si ves una IP que empieza por `169.254.x.x`, es una IP **APIPA** (el servidor DHCP no respondió).
3.  **¿Llego al Router?** `ping 192.168.1.1`.
4.  **¿Llego a Internet?** `ping 8.8.8.8`.
5.  **¿Funciona el DNS?** `nslookup google.com`.
6.  **¿Dónde se corta la ruta?** `tracert 8.8.8.8`.
