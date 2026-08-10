# 0501 Â· MÃ³dulo 1: Riesgos de Seguridad

> Curso 05 Â· MÃ³dulo 1 de 6 Â· Temas: trÃ­ada CIA, malware, ataques a la red e ingenierÃ­a social

---

## Objetivos de este mÃ³dulo

- [ ] Explicar la trÃ­ada CIA con ejemplos
- [ ] Identificar los tipos de malware y sus vectores de infecciÃ³n
- [ ] Conocer los ataques de red clÃ¡sicos
- [ ] Defenderme de la ingenierÃ­a social

---

## 1. La trÃ­ada CIA (el fundamento de la seguridad)

![TrÃ­ada CIA](./diagramas/triada-cia.svg)

| Pilar | Significa | Ejemplo de fallo |
|-------|-----------|------------------|
| **Confidencialidad** | Solo quien debe, puede ver | Fuga de datos personales |
| **Integridad** | Los datos no se alteran | Cambian tus cifras sin que se note |
| **Disponibilidad** | Los servicios responden | Ransomware o DDoS apagan el sistema |

**Conceptos de riesgo**:
- **Amenaza**: cualquier cosa que puede causar daÃ±o (hacker, malware, incendio).
- **Vulnerabilidad**: debilidad que la amenaza explota (SO sin parches).
- **Riesgo**: probabilidad Ã— impacto de que exploten una vulnerabilidad.
- **MitigaciÃ³n**: reducir la probabilidad o el impacto (parches, backups, MFA).

---

## 2. Malware â€” el zoologico

| Tipo | Comportamiento | Ejemplo cÃ©lebre |
|------|----------------|------------------|
| **Virus** | Se adjunta a archivos ejecutables | ILOVEYOU |
| **Gusano (Worm)** | Se autorreplica por red sin clic | WannaCry |
| **Troyano** | Se disfraza de software legÃ­timo | Emotet |
| **Ransomware** | Cifra tus datos y pide rescate | WannaCry, LockBit |
| **Spyware / keylogger** | EspÃ­a actividad y roba credenciales | Pegasus (espionaje) |
| **Rootkit** | Se oculta en el sistema | Bootkits |
| **Botnet** | Tu equipo se une a un ejÃ©rcito controlado | Mirai (IoT) |

**Vectores de infecciÃ³n** (cÃ³mo entra):
1. **Phishing** (correo/WhatsApp con enlaces o adjuntos) â€” el nÂº1 mundial.
2. Descargas de sitios falsos y "cracks".
3. Vulnerabilidades sin parchear.
4. USB infectados.
5. Malvertising (anuncios venenosos), drive-by downloads, exploits de navegador.

> **Caso real (el que ya vivimos)**: un `.bat` de una supuesta app financiera descargado de un anuncio falso â†’ cuarentena + anÃ¡lisis + rotaciÃ³n de contraseÃ±as + runbook. La defensa funciona en cadena.

---

## 3. Ataques de red clÃ¡sicos

| Ataque | CÃ³mo funciona | Defensa |
|--------|---------------|---------|
| **DoS / DDoS** | Saturar recursos hasta caer | Firewalls, rate limiting, CDN |
| **Man-in-the-Middle** | Intercepta tu trÃ¡fico | HTTPS/TLS, VPN, no usar Wi-Fi pÃºblico abierto |
| **Packet sniffing** | Lee tramas en la red | Cifrado (no se puede leer lo cifrado) |
| **Ataque de diccionario / fuerza bruta** | Probar contraseÃ±as | Bloqueo de intentos + 2FA |
| **Replay** | Reutiliza datos captados | Nonces/timestamps en los protocolos |
| **Port scanning** | Reconocimiento de puertos abiertos | Firewall + no exponer servicios innecesarios |

---

## 4. IngenierÃ­a social â€” el malware "de humanos"

El **80% de los incidentes** empiezan con un humano engaÃ±ado, no con tecnologÃ­a.

| TÃ©cnica | SeÃ±al de alerta | Defensa |
|---------|-----------------|---------|
| **Phishing** (correo) | Remitente raro, urgencia, errores | Verificar dominio, no abrir adjuntos, reportar |
| **Smishing/vishing** (SMS/voz) | "Tu banco te llama", cÃ³digos | Colgar y llamar al banco tÃº mismo |
| **Pretexting** | Una historia para que des datos | Nunca dar credenciales por telÃ©fono |
| **Baiting** | USB "encontrado" en el parqueo | Nunca conectar dispositivos desconocidos |
| **Whaling** | SuplantaciÃ³n del jefe (CEO) | Confirmar por segundo canal |

**3 reglas de oro para enseÃ±ar a los usuarios**:
1. **Ninguna entidad legÃ­tima pide tu contraseÃ±a o cÃ³digo por mensaje/llamada.**
2. Urgencia + presiÃ³n = fraude. Detente, verifica por otro canal.
3. Ante la duda: **no hagas clic**, reporta a TI.

---

## PrÃ¡ctica del mÃ³dulo

1. Inventa 3 correos de phishing (uno de banco, uno de "premio", uno del "jefe") y anota quÃ© trampas usaste â€” luego pÃ­dele a alguien que los detecte.
2. Busca ejemplos reales: *"ejemplos phishing banco EspaÃ±a/real email"* y analiza las seÃ±ales.
3. En tu equipo: revisa los adjuntos que no debes abrir: `.exe .bat .scr .vbs .js .msi` comprimidos.
4. Defiende a tu familia: explica la regla nÂº1 con un ejemplo real cotidiano.

## Plataformas gratuitas para practicar

- **TryHackMe** (https://tryhackme.com): rooms gratuitas de phishing y redes
- **Phishing quiz**: busca *"phishing quiz sony"* o *"google phishing quiz"* (juego oficial de Google)
- **picoCTF** (https://picoctf.org): retos iniciales de seguridad

---

## Checklist de dominio â€” MÃ³dulo 1

- [ ] Explico CIA con 3 ejemplos cotidianos
- [ ] Reconozco cada tipo de malware y cÃ³mo entra
- [ ] Describo DDoS, MitM y fuerza bruta con defensas
- [ ] Detecto phishing sin abrir nada
- [ ] Aplico la regla de "verificar por segundo canal"
- [ ] Sigo el flujo de respuesta ante un correo sospechoso (reportar)

