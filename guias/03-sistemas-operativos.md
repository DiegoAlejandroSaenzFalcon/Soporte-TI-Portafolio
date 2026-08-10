# 03 · Sistemas Operativos

> Guía práctica de conocimiento · Administración y diagnóstico

---

## 1. Anatomía de un Sistema Operativo
*   **Kernel (Núcleo)**: único programa que gestiona memoria, procesos, dispositivos y comunicación entre hardware y software.
*   **Espacio de Kernel vs Espacio de Usuario**: aislamiento entre lo crítico y las aplicaciones (protección contra fallos/crashes).
*   **Procesos**: cada programa en ejecución tiene un PID (Process ID); el SO controla prioridades, CPU y memoria.
*   **Boot (Arranque)**: BIOS/UEFI → POST → bootloader (GRUB/Windows Boot Manager) → carga el kernel → `init`/`systemd`.
    *   **UEFI** reemplaza a BIOS (arranque más rápido, particiones GPT, Secure Boot).
    *   **MBR vs GPT**: esquemas de partición; GPT es el estándar moderno (soporta +2 TB).

---

## 2. Usuarios, Grupos y Permisos
*   **Windows**: cuentas locales/Dominio, **UAC**, grupos (`Administrators`, `Users`), `icacls`.
*   **Linux**: `sudo`, grupos (`sudo`, `www-data`), permisos rwx:
    *   `chmod 755` → dueño: rwx · grupo: rx · otros: rx
    *   **ACL**: permisos granulares adicionales (`setfacl/getfacl`).
*   Regla de oro: **Principio de Mínimo Privilegio** (solo lo que se necesita, solo cuando se necesita).

---

## 3. Gestión de Procesos y Servicios
| Acción | Windows | Linux |
| :--- | :--- | :--- |
| Listar procesos | `tasklist` / Administrador de tareas | `ps aux`, `top`, `htop` |
| Matar un proceso | `taskkill /PID 123 /F` | `kill -9 123` |
| Servicios | `services.msc`, `sc` | `systemctl` (systemd) |
| Iniciar con el sistema | `Sysinternals Autoruns` | `systemctl enable foo` |

*   Problemas típicos: proceso colgado (100% CPU) → identificar con `top`/Administrador de tareas y reiniciar el servicio.

---

## 4. Almacenamiento y Sistemas de Archivos
*   **Windows**: NTFS estándar (permisos, cifrado EFS, cuotas); FAT32/exFAT para USB.
*   **Linux**: **ext4** estándar; **XFS/Btrfs** para servidores; montaje con `mount`/`fstab`.
*   **Particiones**: `diskpart` (Windows) / `fdisk`, `gdisk` (Linux) — crea, formatea y asigna letras.
*   **Diagnóstico**: `chkdsk` / `fsck` — reglas de comprobación y reparación de discos.
*   `df -h` (uso), `du -sh *` (tamaños), Desfragmentador (solo HDD, nunca SSD).

---

## 5. Memoria y Rendimiento
*   **RAM virtual / Swap / Archivo de paginación**: cuando la RAM física se agota, el SO usa disco como respaldo (lento).
*   **Troubleshooting de lentitud**:
    1. Abrir `Administrador de tareas` / `top` y ordenar por CPU y Memoria.
    2. Identificar el proceso consumidor (ej. navegador con 20 pestañas).
    3. Revisar arranques: `Autoruns`/`systemd-analyze blame`.
    4. Cerrar servicios innecesarios y limpiar archivos temporales.
*   **Pantalla azul (BSOD)** en Windows: anotar el código de error, revisar `dump files` y Event Viewer.

---

## 6. Instalación de Software y Paquetes
| Windows | Linux | 
| :--- | :--- |
| Instaladores `.exe/.msi`, `winget`, `choco`, Microsoft Store | `apt install`, `dnf install`, `pacman -S` |
| Actualizar todo: `winget upgrade --all` | `sudo apt update && sudo apt upgrade` |

*   Preferir siempre fuentes oficiales (evitar cracks/activadores = malware).

---

## 7. Acceso Remoto y Soporte
*   **RDP** (Windows): `mstsc` — puerto 3389, habilita con Network Level Authentication.
*   **SSH** (Linux/servidores): puerto 22, `ssh usuario@ip`, claves públicas (mejor que contraseñas).
*   **TightVNC/AnyDesk/TeamViewer**: escritorio remoto multiplataforma para soporte al cliente.
*   Buenas prácticas: cambiar puertos por defecto, usar VPN/túneles, registrar quién y cuándo accede.