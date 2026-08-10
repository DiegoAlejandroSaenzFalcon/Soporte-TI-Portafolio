# 0206 Â· MÃ³dulo 6: Troubleshooting y Futuro de las Redes

> Curso 02 Â· MÃ³dulo 6 de 6 Â· Temas: caja de herramientas de diagnÃ³stico, nube, IPv6, SDN, IoT

---

## Objetivos de este mÃ³dulo

- [ ] Dominar las herramientas de diagnÃ³stico de red (ping, traceroute, dig, netstat)
- [ ] Resolver los incidentes de red mÃ¡s comunes paso a paso
- [ ] Conocer las tendencias: nube, IPv6, SDN, IoT

---

## 1. La caja de herramientas del tÃ©cnico de redes

| Herramienta | QuÃ© responde | Ejemplo |
|-------------|--------------|---------|
| **ping** | Â¿EstÃ¡ vivo? (ICMP echo) | `ping 8.8.8.8` |
| **traceroute / tracert** | Â¿DÃ³nde se corta la ruta? | `tracert 8.8.8.8` |
| **nslookup / dig** | Â¿Resuelve el DNS? | `nslookup google.com` |
| **netstat / ss** | Â¿QuÃ© conexiones hay? Â¿Escucha este puerto? | `netstat -ano` |
| **ipconfig / ifconfig / ip** | Â¿QuÃ© IP tengo? | `ipconfig /all` |
| **Test-NetConnection** | Â¿Este puerto estÃ¡ abierto? (PowerShell) | `Test-NetConnection sitio -Port 443` |
| **curl** | Â¿Responde el servicio HTTP? | `curl -I https://sitio` |
| **arp** | Â¿QuÃ© MAC hay en mi LAN? | `arp -a` |

### Flujo de diagnÃ³stico profesional
```mermaid
flowchart TD
    A[Problema: no hay conexion] --> B{Â¿IP valida? ipconfig}
    B -- APIPA 169.254 --> C[DHC P fallo: revisar cable / reiniciar router]
    B -- IP normal --> D{Â¿Ping al gateway?}
    D -- No --> E[Red local: cable, Wi-Fi, router]
    D -- Si --> F{Â¿Ping a 8.8.8.8?}
    F -- No --> G[ISP / acceso: reinicio modem, soporte ISP]
    F -- Si --> H{Â¿Resuelve DNS? nslookup}
    H -- No --> I[DNS: flushdns, cambiar DNS]
    H -- Si --> J{Â¿Responde el servicio? puerto 443}
    J -- No --> K[Servidor/aplicacion: avisar al responsable]
    J -- Si --> L[Todo OK: problema especifico del equipo/app]
```

![El viaje de un dato por las 5 capas](./diagramas/viaje-dato-5-capas.svg)

---

## 2. Incidentes tÃ­picos y sus causas â„–1

| SÃ­ntoma | Causa mÃ¡s probable | Primera acciÃ³n |
|---------|--------------------|----------------|
| Internet lenta en todo | SaturaciÃ³n ISP / Wi-Fi congestionado | Speedtest + probar por cable |
| Internet lenta en un equipo | Antivirus/actualizaciones en segundo plano | Revisar uso de red (`taskmgr`) |
| Sitio no carga, otros sÃ­ | DNS o firewall del equipo | flushdns + probar otro DNS |
| Red intermitente | SeÃ±al Wi-Fi dÃ©bil / canal saturado | Canal 1/6/11, banda 5 GHz |
| Sin IP (169.254) | DHCP no contesta | Reiniciar router, revisar cable |
| Un servicio no responde | Firewall o puerto mal configurado | Test-NetConnection puerto |

---

## 3. El futuro de las redes (para estar al dÃ­a)

### Nube (Cloud Computing)
- **PÃºblico**: AWS, Azure, GCP â€” infraestructura alquilada (IaaS/PaaS/SaaS).
- **Privado/hÃ­brido**: infraestructura propia + nube.
- **Colocation / hiperescala / borde (edge)**: dÃ³nde viven los datos hoy.
- Ventajas: escala, pago por uso, resiliencia global.

### IPv6 â€” la migraciÃ³n
- Mitiga el agotamiento de IPv4; **doble pila** convive hoy.
- AutomÃ¡tica (**SLAAC**) sin servidor DHCP clÃ¡sico.
- Comandos: `ping6`, `ip -6 addr`.

### SDN (Redes Definidas por Software)
- La **lÃ³gica** (control) se separa del **hardware** (envÃ­o): centralizado y programable.
- Beneficio: configurar toda la red con cÃ³digo (network-as-code).

### IoT (Internet de las Cosas)
- Miles de dispositivos pequeÃ±os conectados: sensores, cÃ¡maras, electrodomÃ©sticos.
- **Riesgo de seguridad**: muchos IoT son inseguros por defecto â†’ segmÃ©ntalos en una red separada (VLAN de invitados).
- EstÃ¡ndares: Zigbee, LoRaWAN, NB-IoT, Matter.

---

## 4. Laboratorio final del curso (integrador)

DiseÃ±a y arma en **Packet Tracer**:
1. 3 subredes interconectadas con 2 routers (IPs estÃ¡ticas correctas).
2. Un servidor DNS + DHCP + web en una subred.
3. PCs en DHCP automÃ¡tico, con DNS que resuelve el sitio local.
4. Regla de firewall que permite HTTP pero bloquea otro puerto.
5. VerificaciÃ³n final: `ping` PCâ†’PC entre subredes y navegaciÃ³n al servidor.

Toma capturas del laboratorio â†’ son material de portafolio profesional (como este guÃ­a).

---

## Checklist de dominio â€” MÃ³dulo 6

- [ ] Corro un diagnÃ³stico completo (IP â†’ gateway â†’ Internet â†’ DNS â†’ puerto) sin ayuda
- [ ] Explico quÃ© me dice cada comando de la caja de herramientas
- [ ] Resuelvo "sitio no carga pero Internet funciona" en minutos
- [ ] Explico nube pÃºblica/privada/hÃ­brida y SDN en tÃ©rminos simples
- [ ] Digo por quÃ© IPv6 existe y quÃ© es la doble pila
- [ ] Completo el laboratorio integrador de Packet Tracer

---

## Fin del Curso 02 â€” Siguiente paso
Completa el examen del curso (opcional) y continÃºa con **Curso 03 Â· Sistemas Operativos** â†’
