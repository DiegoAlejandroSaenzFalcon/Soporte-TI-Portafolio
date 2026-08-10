# 0301 · Módulo 1: Navegando el Sistema

> Curso 03 · Módulo 1 de 6 · Temas: sistema de archivos, rutas, navegación y conexiones remotas

---

## Objetivos de este módulo

- [ ] Entender la estructura de archivos de Windows y Linux
- [ ] Navegar con la línea de comandos sin miedo
- [ ] Instalar un SO correctamente (VM y real)
- [ ] Conectar equipos remotos (SSH, RDP, FTP)

---

## 1. La estructura de archivos

### Windows
| Ruta | Contenido |
|------|-----------|
| `C:\Windows` | Archivos del sistema |
| `C:\Program Files` / `Program Files (x86)` | Aplicaciones (64/32 bits) |
| `C:\Users\<usuario>` | Perfiles: Desktop, Documents, Downloads |
| `%AppData%` | Configuración de aplicaciones del usuario |
| `C:\Windows\System32` | DLLs y herramientas del sistema |

### Linux (todo dentro de `/`)
| Ruta | Contenido |
|------|-----------|
| `/home/usuario` | Archivos personales (~) |
| `/etc` | Configuración del sistema |
| `/var` | Datos variables (logs: `/var/log/syslog`) |
| `/usr` | Programas del sistema |
| `/bin`, `/sbin` | Ejecutables |
| `/tmp` | Archivos temporales |
| `/dev` | Dispositivos (como archivos) |

**Ruta absoluta** (desde la raíz, `C:\` o `/`) vs **relativa** (desde donde estás). `.` = aquí, `..` = carpeta padre.

---

## 2. Navegación por comandos

| Acción | Windows (PS/CMD) | Linux (bash) |
|--------|------------------|--------------|
| ¿Dónde estoy? | `pwd` (PowerShell) / `cd` | `pwd` |
| Listar | `ls`, `dir` | `ls -la` |
| Cambiar carpeta | `cd`, `cd ..` | `cd`, `cd ..` |
| Tocar archivo | `New-Item archivo` | `touch archivo` |
| Ver contenido | `type`, `Get-Content` | `cat archivo` |
| Copiar/mover | `Copy-Item`, `Move-Item` | `cp`, `mv` |
| Borrar | `Remove-Item` | `rm -rf` (¡cuidado!) |
| Buscar | `Get-ChildItem -Recurse` | `find`, `grep` |

> **Regla de oro**: `rm -rf` borra sin preguntar y "con poder" — jamás lo uses a ciegas. `sudo` en Linux implica privilegios de administrador: úsalo solo cuando sea necesario.

---

## 3. Instalación de un SO (recapitulación práctica)

1. **Windows**: crear **USB de arranque** (Rufus/Microsoft Media Creation Tool) → arrancar desde USB (menú F12/F2/Del) → instalador (clave, partición, usuario).
2. **Linux**: ISO de Ubuntu/Debian → VM (VirtualBox) o USB → instalador.
3. **máquina virtual**: perfecta para practicar sin riesgo (snapshots = viajes en el tiempo).

**Arranque dual**: Windows + Linux en el mismo equipo con GRUB eligiendo al encender — útil pero con riesgo de perder datos si no se particiona bien (practica antes en VM).

---

## 4. Conexiones remotas (el pan de cada día del soporte)

| Herramienta | Uso | Puerto |
|-------------|-----|--------|
| **SSH** | Consola remota segura (Linux/servidores) | 22 |
| **RDP** | Escritorio remoto gráfico Windows | 3389 |
| **VNC / AnyDesk / TeamViewer** | Soporte remoto multiplataforma | varios |
| **SFTP / FTP** | Transferencia de archivos | 22 / 21 |

```powershell
ssh usuario@192.168.1.100          # Linux: conexión con password
ssh -i clave.pem usuario@servidor   # con clave privada
mstsc                              # Windows: cliente RDP
```

> **Seguridad**: cambia contraseñas por **claves SSH** cuando sea posible; para RDP usa siempre *Network Level Authentication* y no expongas el puerto 3389 directo a Internet (usa VPN).

---

## Práctica del módulo

1. En tu PC: navega `C:\Users`, `C:\Windows\System32`; explora `%AppData%`.
2. En la VM Linux: `cd /etc && ls && cat os-release`.
3. Crea un árbol de carpetas por comandos y bórralo con cuidado (`.` y `..`).
4. Conecta por SSH a tu VM Linux desde Windows (`ssh usuario@IP-VM`) si configuras el servicio ssh.

## Plataformas gratuitas para practicar

- **VirtualBox** (https://www.virtualbox.org) + ISO Ubuntu (https://ubuntu.com)
- **OverTheWire: Bandit** (https://overthewire.org) — terminal Linux por niveles
- **Linux Journey** (https://linuxjourney.com) — navegación y comandos interactivos

---

## Checklist de dominio — Módulo 1

- [ ] Dibujo de memoria la estructura de archivos de ambos SO
- [ ] Navego y opero archivos por CLI sin dudar
- [ ] Instalé Linux en una VM y Windows (real o VM) una vez
- [ ] Entiendo qué es una ruta absoluta vs relativa
- [ ] Conecto por SSH/RDP de forma segura
- [ ] Respeto las reglas de oro de `sudo` y `rm -rf`