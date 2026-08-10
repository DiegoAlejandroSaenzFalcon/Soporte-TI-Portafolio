# 0306 · Módulo 6: Sistemas Operativos en la Práctica

> Curso 03 · Módulo 6 de 6 · Temas: troubleshooting real de SO: arranque, malware, herramientas y escenarios

---

## Objetivos de este módulo

- [ ] Resolver problemas de arranque (modo seguro, reparación)
- [ ] Diagnosticar los errores clásicos de Windows y Linux
- [ ] Aplicar un flujo integral anti-malware
- [ ] Usar herramientas de recuperación sin perder datos

---

## 1. Problemas de arranque (el susto nº1 del usuario)

| Síntoma | Causa típica | Solución inicial |
|---------|--------------|------------------|
| No enciende nada | Fuente/cable | Ver PSU, botón, luz de la placa |
| Pantalla negra + beeps | RAM mal asentada / GPU | Reasentar RAM (limpia contactos) |
| Carga y se reinicia | Disco dañado / SO roto | Reparación de inicio |
| "Bootmgr missing" (Win) | Boot corrupto | Reparar con USB de Windows |
| "GRUB rescue" (Linux) | Bootloader roto | Reinstalar GRUB (`grub-install`) |
| Arranque infinito | Driver malo / malware | Modo seguro + desinstalar |

**Modo seguro (Windows)**: `shift + reiniciar` → Solucionar problemas → Opciones avanzadas → Reparación de inicio / Modo seguro. En Linux: agregar `single`/`recovery` como parámetro de arranque en GRUB.

**Copia de seguridad ANTES de cualquier reparación mayor** — regla absoluta.

---

## 2. Los clásicos de diagnóstico

```powershell
# Windows
eventvwr              # Visor de eventos: errores críticos (Application y System)
msinfo32              # Resumen completo del equipo
sfc /scannow          # Verifica/repare archivos del sistema
DISM /Online /Cleanup-Image /RestoreHealth   # Repara la imagen de Windows
```
```bash
# Linux
dmesg | grep -i error   # Errores del kernel
journalctl -p err -b     # Errores del arranque actual (systemd)
systemctl --failed       # Servicios que fallaron
fsck /dev/sdb1           # Verificar FS (desmontado)
```

| Error | Respuesta |
|-------|-----------|
| "BSOD 0x0000007B" (Windows) | Disco/SATA/controlador → revisar disco y BIOS |
| Kernel panic (Linux) | Kernel malsano → arrancar kernel anterior |
| "Falta una DLL / lib" | Reinstalar la app o reparar con sfc/repos |
| `initramfs` falla (Linux) | Actualizar initramfs o reparar fstab |

---

## 3. Flujo integral ante malware (nivel de campo)

```mermaid
flowchart TD
    A[Usuario: "mi PC esta rara"] --> B[1. Aislar: desconectar de red\nno usar mas el equipo]
    B --> C[2. Arrancar en modo seguro con red]
    C --> D[3. Escaneo completo antivirus definido\nDefender + segunda opinion (Malwarebytes)]
    D --> E{¿Deteccion?}
    E -- Si --> F[Cuarentena y eliminacion\nrevisar inicio y tareas programadas]
    E -- No pero sigue raro --> G[Revisar Autoruns / procesos\ncarpetas AppData temporales\nanalizar con online scanners]
    F --> H[4. Rotar contraseñas importantes\nen OTRO equipo seguro]
    G --> H
    H --> I[5. Verificar restauracion y\nactualizar todo antes de devolver al usuario]
    I --> J[6. Documentar el incidente\n - runbook para la proxima]
```

**Puntos de persistencia** (dónde se esconden): Registro (Run), carpetas `AppData\Roaming`, tareas programadas, servicios, extensiones del navegador. Herramientas: **Sysinternals Autoruns** (gold standard de arranques).

**Checks rápidos después del escaneo**:
- `msconfig`/Autoruns: inicio limpio.
- Extensiones del navegador desconocidas → eliminar.
- `net user`/cuentas: ¿hay cuentas nuevas? (posible backdoor).
- Windows Defender Firewall: reglas de salida raras.

---

## 4. Recuperación sin perder datos

| Herramienta | Uso |
|-------------|-----|
| **Puntos de restauración** (Windows) | Volver el sistema a un estado sano |
| **Reparación de inicio** | Reparar boot sin reinstalar |
| **Copia del disco a otro** | Clonezilla / dd si el disco muere |
| **Live USB Linux** (Ubuntu live) | Arrancar sin tocar el disco: rescatar archivos, `fsck`, copia de seguridad |
| **`dd` (Linux)** | Clonado/imagen de disco a nivel de bloque |
| **Archivos de respaldo** | La única solución 100% efectiva |

> **Live USB** es la navaja suiza: se arranca desde el USB, se monta el disco del cliente fastidiado y se copian sus documentos a un disco externo antes de cualquier reparación.

---

## 5. Escenarios integradores (tipo examen)

1. **"Mi computador arranca, veo el logo y se reinicia"** → modo seguro → desinstalar última actualización/driver → sfc → puntos de restauración.
2. **"Mi computador está lentísima y se abren páginas raras"** → aislar → escaneo → Autoruns → rotar contraseñas → documentar.
3. **"No me entra Windows, necesito mis documentos"** → Live USB → copiar documentos → reparar boot o reinstalar.
4. **"El servidor de la oficina no arranca a Linux"** → GRUB rescue → `ls (hd0,gpt2)` → `set root`/`insmod` → `grub-install` (o reinstalar GRUB con live).

---

## Práctica final del módulo

1. Crea un **punto de restauración** en tu Windows y verifica que existe.
2. Levanta tu VM Linux en "modo de recuperación" y navega el initramfs.
3. Descarga **Autoruns** (Sysinternals) y analiza los arranques de tu equipo.
4. Arma tu **USB Live de Ubuntu** (Rufus/BalenaEtcher) como herramienta de rescate profesional.

## Plataformas gratuitas para practicar

- **Sysinternals Suite** (https://learn.microsoft.com/sysinternals): Autoruns, Process Explorer
- **VirtualBox + Ubuntu Live** para prácticas de rescate
- **TryHackMe / picoCTF**: rooms de análisis básico de malware (conceptos)
- **NetAcad IT Essentials**: escenarios finales de sistemas operativos

---

## Checklist de dominio — Módulo 6

- [ ] Entro en modo seguro y reparo un inicio dañado en ambos SO
- [ ] Leo el Visor de eventos / journalctl sin miedo
- [ ] Aplico el flujo anti-malware completo (aislar → escanear → rotar → documentar)
- [ ] Busco persistencia con Autoruns/registro/tareas
- [ ] Rescato archivos con Live USB antes de reparar
- [ ] Documento cada caso para la base de conocimiento

---

## Fin del Curso 03 — Siguiente paso
Completa el examen del curso (opcional) y continúa con **Curso 04 · Administración de Sistemas e Infraestructura** →