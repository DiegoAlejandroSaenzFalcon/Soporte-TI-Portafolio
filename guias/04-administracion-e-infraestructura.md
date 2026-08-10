# 04 · Administración de Sistemas e Infraestructura TI

> Guía práctica de conocimiento · Sysadmin / Datacenter

---

## 1. El Rol del Administrador de Sistemas
*   **Tareas**: aprovisionar usuarios, mantener servidores, backups, parcheo, monitoreo, resolución de incidentes, documentación.
*   **Infraestructura TI**: servidores, red, almacenamiento, bases de datos, aplicaciones y el personal que las opera.
*   Metas: **disponibilidad (uptime)**, **fiabilidad**, **rendimiento** y **seguridad**.

---

## 2. Virtualización y Nube
*   **Hipervisores**:
    *   **Tipo 1 (bare-metal)**: ESXi, Hyper-V, Proxmox — corre directamente sobre el hardware (datacenters).
    *   **Tipo 2 (alojado)**: VirtualBox, VMware Workstation — corre sobre un SO existente (pruebas).
*   **Contenedores**: Docker/Kubernetes — entornos ligeros y aislados (misma kernel, app + dependencias).
*   **Nube**:
    *   **IaaS** (AWS EC2, Azure VM, GCP Compute): infraestructura virtual.
    *   **PaaS** (App Service, Heroku): plataforma gestionada.
    *   **SaaS** (Office 365, Gmail, Dropbox): software como servicio.
*   Ventajas: escalado, pago por uso, alta disponibilidad sin comprar hardware.

---

## 3. Servicios de Directorio y Autenticación
*   **Active Directory (AD)** — Windows:
    *   **Dominio**: ámbito administrativo de usuarios/equipos; controladores de dominio (DC).
    *   **GPO (Group Policy Objects)**: configurar en masa (políticas de contraseñas, mapeos de red, wallpapers).
    *   **LDAP**: protocolo para leer/modificar el directorio.
*   **Linux**: LDAP + Kerberos / FreeIPA como alternativas.
*   **Aprovisionamiento**: crear usuario estándar → asignar grupos → permisos de carpetas → correo → licencias. **Desaprovisionamiento** al salir: desactivar, auditar, eliminar.

---

## 4. Redes de Datacenter
*   **Servidores**: dedicados (DB, web, correo, archivos) — separar roles por máquina o VM.
*   **DNS interno**: resolver nombres de dominio corporativo (zonas forward/reverse).
*   **DHCP centralizado**: un solo punto de configuración IP para toda la red.
*   **Balanceadores de carga**: distribuyen tráfico entre servidores (alta disponibilidad).
*   **Monitoreo**: CPU, memoria, disco, red — herramientas: Nagios, Zabbix, PRTG, Grafana + Prometheus. Alertas → accionar antes de que el usuario reporte.

---

## 5. Backups y Recuperación ante Desastres (DR)
*   Tipos de backup:
    *   **Completo (Full)**: todo los datos — lento, pero recuperación rápida.
    *   **Incremental**: solo lo cambiado desde el último backup (cualquiera).
    *   **Diferencial**: solo lo cambiado desde el último **full**.
*   **Regla 3-2-1**: 3 copias · 2 medios distintos · 1 copia fuera del sitio.
*   **RPO (Recovery Point Objective)**: cuántos datos puedes perder (tiempo máximo entre backups).
*   **RTO (Recovery Time Objective)**: cuánto tiempo tarda el sistema en volver.
*   **Prueba los backups**: un backup que no se restaura no existe.

---

## 6. Parcheo y Ciclo de Vida del Software
*   Establecer **ventanas de mantenimiento** (semanal/mensual) y política de **compatibilidad** (un parche atrás por razones justificadas).
*   Proceso: probar en entorno de staging → desplegar por fases → verificar → documentar.
*   Herramientas: WSUS/SCCM o Intune (Windows), Landscape/Ansible (Linux), GPO/System Center.

---

## 7. Registros (Logs) y Análisis de Incidentes
*   **Windows**: Event Viewer (`Application`, `Security`, `System`); IDs útiles (4624 inicio de sesión, 4634 cierre, 4688 creación de proceso).
*   **Linux**: `/var/log/syslog`, `dmesg`, `journalctl` (systemd).
*   **Centralización**: Syslog/SIEM (Graylog, Splunk) para correlacionar eventos en toda la infra.
*   **Metodología de troubleshooting**: 1) Definir el problema → 2) Recopilar datos → 3) Formular hipótesis → 4) Probar → 5) Documentar (evita arreglos a ciegas).

---

## 8. Confiabilidad de Servidores
*   **RAID** (redundancia de discos):
    *   RAID 0: rendimiento, sin redundancia.
    *   RAID 1: espejo (2 discos).
    *   RAID 5: paridad distribuida (3+ discos).
    *   RAID 10: espejo + división (rendimiento + redundancia).
*   **UPS** y alimentación redundante para mantenimiento de uptime; enfríamiento y monitoreo físico del rack.