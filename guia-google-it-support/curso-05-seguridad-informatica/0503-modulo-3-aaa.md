# 0503 · Módulo 3: Autenticación, Autorización y Contabilidad (AAA)

> Curso 05 · Módulo 3 de 6 · Temas: identidad, contraseñas, 2FA, permisos y auditoría

---

## Objetivos de este módulo

- [ ] Explicar AAA: autenticación, autorización y contabilidad
- [ ] Diseñar políticas de contraseñas fuertes
- [ ] Configurar 2FA/MFA en servicios
- [ ] Entender permisos y auditoría de accesos

---

## 1. El modelo AAA (los tres filtros)

```mermaid
flowchart LR
    A[Usuario\n"soy juan"] -->|1. AUTENTICACION\n¿quien eres?| B[Credenciales validas]
    B -->|2. AUTORIZACION\n¿que puedes hacer?| C[Permisos y grupos]
    C -->|3. CONTABILIDAD\nauditoria registrada| D[Logs de accion]
```

| Pilar | Pregunta | Ejemplo |
|-------|----------|---------|
| **Autenticación** | ¿Quién eres? | Usuario + contraseña + 2FA |
| **Autorización** | ¿Qué puedes hacer? | Acceso a carpeta, sudo, grupos |
| **Contabilidad** | ¿Qué hiciste? | Logs: quién entró, cuándo, qué tocó |

---

## 2. Factores de autenticación

| Factor | Algo que... | Ejemplos |
|--------|-------------|----------|
| **1º** | ...sabes | Contraseña, PIN |
| **2º** | ...tienes | Token, YubiKey, app autenticadora, SMS |
| **3º** | ...eres | Huella, rostro, iris |

**2FA/MFA**: combina 2 o más factores → si roban tu contraseña, la cuenta sigue protegida. Es **la defensa individual más efectiva** de todas.

**Reglas de contraseñas modernas** (aviso NIST/corporativo):
- Longitud importa más que complejidad: **12+ caracteres**.
- Frases de paso (passphrases): "LaGallinaPoneHuevos2026!" es fuerte y recordable.
- **Única por servicio**: un gestor de contraseñas (Bitwarden, 1Password, Google/Apple) — nunca reutilizar.
- NO cambiar por calendario obligatorio sin motivo (NIST desaconseja rotación forzosa frecuente); sí rotar **inmediatamente** ante sospecha de compromiso.
- Sin preguntas de seguridad con respuestas públicas.

---

## 3. Autorización: el mínimo privilegio

| Concepto | Práctica |
|----------|----------|
| **Mínimo privilegio** | Solo lo necesario para su rol |
| **RBAC** | Permisos por roles/grupos, no por persona |
| **Cuentas administrativas** | Usarlas solo para administrar (no para el día a día) |
| **Separación de tareas** | Quien aprueba ≠ quien ejecuta (finanzas/deploy) |
| **Temporalidad** | Accesos con caducidad o revisión periódica |

**Ejemplo aplicado**: el contador puede **leer** la carpeta ventas (no editar); soporte puede instalar programas pero no tocar RRHH; el administrador entra como admin solo cuando administra.

---

## 4. Contabilidad y auditoría (el registro lo es todo)

| Dónde se registra | Qué ver |
|--------------------|---------|
| Windows Event Viewer · Seguridad | 4624 (inicio sesión), 4634/4647 (cierre), 4720+ (usuarios) |
| Linux `last` / `/var/log/auth.log` | Quién inició sesión y desde dónde |
| Servicios cloud | Reportes de sign-in (Azure AD, Google Admin) |
| **SIEM** (avanzado) | Centraliza y correlaciona (Graylog, Splunk, Wazuh) |

**Detecciones útiles**: inicios de sesión a horas raras, desde países imposibles, éxitos tras 20 fallos (fuerza bruta), cuentas nuevas de admin no autorizadas.

> **Para el soporte diario**: ante "me hackearon el correo", lo primero que pides son los **logs de acceso** — con ellos sabes si fue fuerza bruta, phishing o clave reutilizada en otra parte.

---

## 5. Password manager y flujo de la cuenta comprometida

### Gestor de contraseñas: cómo venderlo
| Argumento | Frase |
|-----------|-------|
| Reutilización | "Una clave para todo = una puerta para todo" |
| Fuerza | "Cada cuenta con una clave de 16 caracteres generada por el gestor" |
| MFA | "El gestor + 2FA = tus cuentas blindadas" |

### Flujo de respuesta (cuenta comprometida)
1. Aislar: cerrar sesiones de todos los dispositivos (Google/Apple/Microsoft + "cerrar sesión en todas partes").
2. Rotar la contraseña DE LA CUENTA y de las cuentas que la reutilizaban.
3. Activar 2FA si no estaba; regenerar tokens/API keys.
4. Revisar correos/carpetas sensibles y configuración (redirecciones, reglas nuevas).
5. Escanear el dispositivo que la tenía (posible origen).
6. Documentar + monitorizar sign-ins raros las siguientes 2 semanas.

---

## Práctica del módulo

1. Activa 2FA en 3 servicios tuyos (correo, banca, redes) — hazlo hoy mismo.
2. Instala un gestor de contraseñas (Bitwarden) y rota las 3 contraseñas más reutilizadas.
3. En tu VM: mira `/var/log/auth.log` / `last` y encuentra tus propias conexiones.
4. En Windows: revisa el Visor de eventos → Seguridad (evento 4624) de sesiones recientes.
5. Revisa tus sesiones activas en Google/bancos (opción "tus dispositivos") y cierra las que no reconozcas.

## Plataformas gratuitas para practicar

- **Bitwarden** (https://bitwarden.com) — gestor de contraseñas de código abierto
- **TryHackMe — Authentication and AAA rooms** (https://tryhackme.com)
- **Microsoft Learn — Entra ID security** (https://learn.microsoft.com)
- Google: buscas *"security checkup google"* — auditoría gratuita de tus cuentas

---

## Checklist de dominio — Módulo 3

- [ ] Explico AAA con un ejemplo real de oficina
- [ ] Configuro MFA y sé enseñarlo a un usuario
- [ ] Diseño una política de contraseñas moderna (longitud + gestor, sin rotación forzosa)
- [ ] Aplico mínimo privilegio con RBAC en un caso concreto
- [ ] Leo logs de acceso para investigar un acceso sospechoso
- [ ] Ejecuto el flujo de recuperación de cuenta comprometida al primer aviso