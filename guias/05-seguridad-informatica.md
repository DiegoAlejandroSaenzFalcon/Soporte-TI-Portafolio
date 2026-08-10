# 05 · Seguridad Informática

> Guía práctica de conocimiento · Defensa operativa

---

## 1. Fundamentos: La Tríada CIA
*   **Confidencialidad**: solo quien debe, puede ver (cifrado, permisos).
*   **Integridad**: los datos no se alteran (hashing, firmas).
*   **Disponibilidad**: los sistemas responden cuando se necesitan (redundancia, backups).
*   **Gestión de Riesgo**: probabilidad × impacto; identificar, evaluar, mitigar, monitorear.

---

## 2. Tipos de Malware
| Tipo | Comportamiento |
| :--- | :--- |
| **Virus** | Se adjunta a archivos y se replica |
| **Gusano (Worm)** | Se propaga solo por la red sin intervención |
| **Troyano** | Se disfraza de software legítimo |
| **Ransomware** | Cifra datos y exige rescate (ej. WannaCry) |
| **Spyware** | Espía actividad y roba datos |
| **Rootkit** | Oculta su presencia a nivel del sistema |
| **Botnet** | Equipo controlado remotamente para ataques |

*   Vectores de entrada: **phishing** (correos maliciosos), sitios falsos, USB infectados, software crackeado, vulnerabilidades sin parchear.

---

## 3. Ataques de Red y de Ingeniería Social
*   **DoS / DDoS**: saturar servicios para indisponibilidad (amplificación, botnets).
*   **Man-in-the-Middle (MitM)**: interceptación de tráfico (Wi-Fi público).
*   **Packet sniffing / Replay**: captura y reutilización de datos (Wireshark).
*   **Phishing/Pharming/Whaling**: suplantación de identidad por correo, DNS falso, altos ejecutivos.
*   **Ataques de diccionario / fuerza bruta**: mitigar con bloqueo de intentos y MFA.
*   Defensa: **desconfiar por defecto**, validar remitentes, verificar URLs, no dar claves nunca, reportar incidentes.

---

## 4. Criptografía Aplicada
*   **Cifrado simétrico (AES)**: misma clave para cifrar/descifrar — rápido (datos en reposo).
*   **Cifrado asimétrico (RSA, ECC)**: par clave pública/privada — firma y cifrado de canal (TLS/HTTPS).
*   **Hashing (SHA-256)**: huella de un archivo — verificar integridad y contraseñas.
*   **TLS**: protege el tráfico web (candado verde): certificados emitidos por CAs confiables (Let's Encrypt, DigiCert).
*   **Certificados**: validación de identidad de sitios; caducados = riesgo → renovar.

---

## 5. Autenticación, Autorización y Contabilidad (AAA)
*   **Autenticación**: ¿quién eres?
    *   Algo que **sabes** (contraseña), algo que **tienes** (token/llavero YubiKey), algo que **eres** (biometría).
    *   **2FA/MFA**: combinar dos o más factores — la defensa #1 frente a robo de contraseñas.
    *   Políticas de contraseñas: longitud (12+), complejidad, rotación prudente, **gestor de contraseñas**.
*   **Autorización**: ¿qué puedes hacer? (permisos/RBAC).
*   **Contabilidad (Auditoría)**: ¿qué hiciste? (logs de acceso).

---

## 6. Defensa Perimetral y de Endpoint
*   **Firewall**: controla tráfico por reglas (puerto/ip/app). Windows Defender Firewall, pfSense, iptables.
*   **Antivirus / EDR**: detección por firmas + comportamiento; mantenlos actualizados y escaneos programados.
*   **IDS/IPS**: detectan/previenen intrusiones (Snort, Suricata).
*   **VPN**: cifra el canal remoto (WireGuard, OpenVPN); clave para el trabajo fuera de oficina.
*   **Proxy**: intermediario/filtro de contenido web.

---

## 7. Endurecimiento (Hardening)
*   **Parcheo continuo**: sistemas y aplicaciones siempre al día.
*   **Mínimo privilegio**: cuentas administrativas solo para tareas administrativas (no trabajar como admin).
*   **Deshabilitar servicios y puertos innecesarios.**
*   **Configuración segura por defecto** (listas de servicios, GPO de seguridad).
*   **Segmentación de red**: separar invitados, IoT y corporativo (VLANs).
*   **Cifrado de disco**: BitLocker, LUKS — protección de datos en equipos perdidos/robados.

---

## 8. Respuesta a Incidentes (NIST)
1.  **Preparación**: runbooks, roles, herramientas, backups verificados.
2.  **Detección y Análisis**: identificar el evento, recolectar evidencia (no tocar nada crítico).
3.  **Contención**: aislar (desconectar de red, cuarentena del equipo/archivo).
4.  **Erradicación**: eliminar el malware, cerrar la vía de entrada, cambiar credenciales comprometidas.
5.  **Recuperación**: restaurar desde backups limpios, verificar funcionamiento normal.
6.  **Post-incidente**: documentar lecciones aprendidas y mejorar defensas.

*   **Evidencia**: preservar registros con fechas, quién, qué, cuándo y cómo — puede ser material legal.

---

## 9. Seguridad Física y Privacidad
*   **Física**: control de acceso al datacenter, CCTV, racks cerrados, destrucción segura de discos.
*   **Privacidad**: proteger datos personales de usuarios (principio de mínima recolección); cumplir normativas (GDPR/HIPAA/Ley 1581 en Colombia); informar al usuario cuando un incidente toque sus datos.

---

## 10. Check-List Rápida para el Soporte Diario
- [ ] ¿El usuario usa 2FA donde aplica?
- [ ] ¿El antivirus está actualizado y con escaneo programado?
- [ ] ¿El sistema operativo está parcheado?
- [ ] ¿Hay backups recientes y probados?
- [ ] ¿Las contraseñas son fuertes y únicas (gestor)?
- [ ] ¿Los accesos remotos usan VPN/autenticación robusta?
- [ ] ¿Los discos están cifrados en portátiles?