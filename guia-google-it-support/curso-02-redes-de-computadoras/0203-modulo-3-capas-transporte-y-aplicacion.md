# 0203 Â· MÃ³dulo 3: Capas de Transporte y AplicaciÃ³n

> Curso 02 Â· MÃ³dulo 3 de 6 Â· Temas: TCP, UDP, puertos, sockets, firewalls y protocolos de aplicaciÃ³n

---

## Objetivos de este mÃ³dulo

- [ ] Explicar TCP vs UDP con ejemplos del mundo real
- [ ] Comprender el Three-Way Handshake
- [ ] Conocer los puertos mÃ¡s importantes de memoria
- [ ] Entender quÃ© es un socket y cÃ³mo funciona un firewall

---

## 1. TCP â€” TransmisiÃ³n confiable

**TCP (Transmission Control Protocol)** garantiza que los datos lleguen completos, en orden y sin duplicados.

| Mecanismo | FunciÃ³n |
|-----------|---------|
| **NÃºmeros de secuencia** | Ordena los datos al llegar |
| **Acuses (ACK)** | El receptor confirma cada segmento |
| **ReenvÃ­o** | Si no llega el ACK a tiempo, se reenvÃ­a |
| **Control de flujo** | El receptor indica cuÃ¡ntos datos aceptar |

### Three-Way Handshake (la llamada de la red)
```mermaid
sequenceDiagram
    Cliente->>Servidor: SYN (Â¿puedo hablar?)
    Servidor->>Cliente: SYN-ACK (sÃ­, y yo tambiÃ©n)
    Cliente->>Servidor: ACK (listo, comenzamos)
    Note over Cliente,Servidor: Datos en ambos sentidosâ€¦
```
![Handshake TCP](./diagramas/handshake-tcp.svg)

**Puerto de origen**: aleatorio (ej. 52413). **Puerto de destino**: el servicio (ej. 443 para HTTPS).

---

## 2. UDP â€” RÃ¡pido y sin garantÃ­as

**UDP (User Datagram Protocol)** no establece conexiÃ³n ni confirma nada: mÃ¡ndalo y ya.

| AplicaciÃ³n | Protocolo | Â¿Por quÃ©? |
|------------|-----------|-----------|
| Video en vivo / llamadas | UDP | Un paquete perdido no justifica esperar; fluidez > perfecciÃ³n |
| Juegos en lÃ­nea | UDP | Baja latencia crÃ­tica |
| DNS | UDP (puerto 53) | Consulta simple, rÃ¡pida |
| DHCP | UDP | Descubrimiento sin conexiÃ³n previa |
| Transferencia de archivos | TCP | Cero errores permitidos |
| Web / correo / bases de datos | TCP | Confiabilidad obligatoria |

**ComparaciÃ³n final**: TCP = carta certificada; UDP = mensaje de voz gritado.

---

## 3. Puertos (las puertas de la red)

| Puerto | Servicio |
|--------|----------|
| 20/21 | FTP |
| 22 | SSH (acceso remoto seguro) |
| 23 | Telnet (antiguo, inseguro) |
| 25 | SMTP (envÃ­o de correo) |
| 53 | DNS |
| 80 | HTTP |
| 110/143 | POP3 / IMAP (entrega de correo) |
| 443 | HTTPS (web segura) |
| 3389 | RDP (escritorio remoto Windows) |

> **Soporte diario**: si un sitio no carga pero el ping funciona, revisa con `netstat -ano` / `Test-NetConnection` si el puerto 443 responde.

---

## 4. Sockets y Firewalls

**Socket** = IP + puerto â†’ identifica una conversaciÃ³n concreta (`192.168.1.50:52413 â†’ 142.250.190.46:443`).

**Firewall**: filtra trÃ¡fico con reglas de los dos sentidos.
- **Denegar por defecto** (whitelist): solo lo permitido pasa â€” el estÃ¡ndar seguro.
- Reglas por IP, puerto, direcciÃ³n y estado (conexiones establecidasâ†’devolver respuestas).

---

## 5. Capa de aplicaciÃ³n: los protocolos que usamos

| Protocolo | FunciÃ³n | Puerto |
|-----------|---------|--------|
| **HTTP/HTTPS** | NavegaciÃ³n web (HTTPS = cifrado TLS) | 80/443 |
| **FTP/SFTP** | Transferencia de archivos (SFTP = seguro) | 21/22 |
| **SMTP** | EnvÃ­o de correo | 25 |
| **POP3 / IMAP** | Recibir correo (IMAP sincroniza en servidor) | 110/143 |
| **DNS** | TraducciÃ³n nombre â†’ IP | 53 |

**VerificaciÃ³n manual** (sin navegador): `curl https://web.capture` o `Test-NetConnection sitio -Port 443`.

---

## PrÃ¡ctica del mÃ³dulo

1. `netstat -ano | findstr :443` (Windows) / `ss -tn` (Linux): observa conexiones TCP activas.
2. `Test-NetConnection google.com -Port 443` (PowerShell): prueba puertos especÃ­ficos.
3. Wireshark: filtro `tcp.port == 443` y observa el handshake SYN/SYN-ACK/ACK en una visita web.
4. Inicia un juego o llamada de video y compara quÃ© puertos UDP usa (`netstat -an | findstr /i udp`).

## Plataformas gratuitas para practicar

- **Wireshark** (https://www.wireshark.org) â€” capturar handshakes "de verdad"
- **TryHackMe â€” Intro to LAN / Port Scanning rooms** (https://tryhackme.com)
- NetAcad *Networking Basics*: mÃ³dulos de capa de transporte

---

## Checklist de dominio â€” MÃ³dulo 3

- [ ] Explico TCP y UDP con ejemplos de servicios reales
- [ ] Narro el three-way handshake paso a paso
- [ ] Conozco los puertos 22, 25, 53, 80, 443, 3389 sin mirar apuntes
- [ ] Explico quÃ© es un socket (IP + puerto)
- [ ] Configuro una regla mental de firewall "denegar por defecto"
- [ ] Verifico un puerto abierto/cerrado con comandos
