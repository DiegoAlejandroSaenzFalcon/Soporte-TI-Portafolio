# 0405 Â· MÃ³dulo 5: Backups y RecuperaciÃ³n de Datos

> Curso 04 Â· MÃ³dulo 5 de 6 Â· Temas: tipos de backup, RAID, replicaciÃ³n, estrategias y disaster recovery

---

## Objetivos de este mÃ³dulo

- [ ] Elegir el tipo de backup adecuado (full/incremental/diferencial)
- [ ] Explicar RAID y elegir el nivel correcto
- [ ] Entender replicaciÃ³n vs backup
- [ ] DiseÃ±ar una estrategia 3-2-1 completa con RPO/RTO

---

## 1. Tipos de backup y su combinaciÃ³n

| Tipo | Respaldas | RecuperaciÃ³n | Ejemplo semanal |
|------|-----------|--------------|-----------------|
| **Completo (Full)** | Todo | La mÃ¡s rÃ¡pida | Domingo |
| **Incremental** | Solo lo nuevo **desde el Ãºltimo backup** (cualquiera) | Necesitas full + todos los incrementales en orden | Lunes-Viernes |
| **Diferencial** | Solo lo nuevo **desde el Ãºltimo full** | Solo full + Ãºltimo diferencial | SÃ¡bado |

```mermaid
flowchart LR
    F[Full domingo] --> I1[Incremental lunes\n100 archivos]
    I1 --> I2[Incremental martes\n20 archivos]
    I2 --> I3[Incremental miercoles\n5 archivos]
```

**CÃ¡lculo de RPO**: con backup diario, pierdes como mÃ¡ximo 24 h de datos (RPO = 24 h). Para RPO menor â†’ backups mÃ¡s frecuentes (cada hora) o replicaciÃ³n continua.

---

## 2. RAID â€” redundancia a nivel de disco

| Nivel | MÃ­n. discos | CÃ³mo funciona | Resultado |
|-------|-------------|---------------|-----------|
| **0** | 2 | Fragmenta (stripe) | + velocidad, **sin** redundancia |
| **1** | 2 | Espejo | 1 disco falla y sigues (50% pÃ©rdida de capacidad) |
| **5** | 3 | Paridad distribuida | 1 disco falla y sigues; buen equilibrio |
| **10** | 4 | Espejo + stripe | RÃ¡pido + tolerante (bases de datos) |

![Niveles de RAID](./diagramas/raid-niveles.svg)

> **RAID â‰  backup**: RAID protege contra **fallo de disco fÃ­sico**, no contra errores humanos, ransomware, incendio o borrado accidental. El ransomware cifra los discos RAID por igual.

---

## 3. ReplicaciÃ³n vs Backup

| Estrategia | QuÃ© hace | RPO/RTO |
|------------|----------|---------|
| **Backup** | Copias en el tiempo (versiones) | Horas/dÃ­as |
| **ReplicaciÃ³n sÃ­ncrona** | Espejo en vivo entre 2 sistemas | Casi cero |
| **ReplicaciÃ³n asÃ­ncrona** | Espejo con ligero retraso (multi-sitio) | Minutos |

**Snapshots (VM)**: instantÃ¡neas de estado de una VM â€” increÃ­bles para rollback rÃ¡pido, pero **no son backup**: viven en el mismo disco/almacÃ©n que la VM.

> **DiseÃ±o ganador**: backups (versiones) + replicaciÃ³n off-site (continuidad) + snapshots (rollback rÃ¡pido) â€” cada capa cubre una amenaza distinta.

---

## 4. La estrategia 3-2-1 (el estÃ¡ndar de oro)

![Regla 3-2-1](./diagramas/backup-3-2-1.svg)

**3 copias** de los datos Â· **2 medios/formatos** distintos Â· **1 copia fuera del sitio**

| Capa | Ejemplo |
|------|---------|
| Copia 1 | Disco local del servidor (producciÃ³n) |
| Copia 2 | NAS local o disco externo (backup programado) |
| Copia 3 | **Nube / otro sitio** (S3, Google Drive cifrado, datacenter) |

**Extra recomendado: 3-2-1-1** â€” la copia off-site debe ser **inmutable o aislada** para sobrevivir a ransomware (los atacantes borran los backups visibles).

---

## 5. Herramientas de backup

| Herramienta | Tipo |
|-------------|------|
| **Veeam** | EstÃ¡ndar de la industria (VM, ruta gratuita limitada) |
| **BorgBackup / restic / Duplicati** | Backup por archivos, cifrado, deduplicaciÃ³n â€” gratuitas y excelentes |
| **`rsync`** | Copia incremental por lÃ­nea de comandos (Linux) |
| **`dd`** | Clonado bruto de discos (imagen completa) |
| **Solutions cloud** | Azure Backup, AWS Backups, Google Vault/Drive, IDrive, Backblaze |
| **Windows Server Backup / ntbackup sucesores** | Sistemas Windows |

```bash
# Ejemplo rsync + cron (backup diario de /var/www y /etc)
rsync -av --delete /var/www/ /backup/www/
rsync -av --delete /etc/ /backup/etc/
# En el crontab: 0 2 * * *  rsync -av ... (02:00 diario)
```

**RestauraciÃ³n**: se prueba, se prueba, se prueba. Un backup sin probar es un diploma de esperanza.

---

## 6. Plan de RecuperaciÃ³n ante Desastres (DR)

```mermaid
flowchart TD
    A[Incidente: servidor muerto] --> B[1. Declarar estado y avisar al negocio\nquien decide, quien actua]
    B --> C[2. Restaurar prioridades: correo, web, datos\nde acuerdo al runbook DR]
    C --> D[3. Restaurar desde backup off-site\nverificar integridad]
    D --> E[4. Prueba de servicios con usuarios reales]
    E --> F[5. Revisar lecciones: que fallo, que mejorar\nactualizar runbook]
```

**RTO del diseÃ±o**: para una PYME, meta razonable = restaurar servicios crÃ­ticos en el mismo dÃ­a (RTO â‰¤ 24 h) y datos con RPO â‰¤ 24 h, mejorable segÃºn crÃ­ticas. **Probar el DR una vez al aÃ±o como mÃ­nimo.**

---

## PrÃ¡ctica del mÃ³dulo

1. Configura un backup automÃ¡tico diario con `rsync` + `cron` en tu VM (carpetas /etc y /var/www).
2. Rompe algo (borra un archivo del repositorio Web) y **restaura** desde tu backup â€” prÃ¡ctica real de restauraciÃ³n.
3. En VirtualBox: crea 3 snapshots de tu VM y vuelve atrÃ¡s; compara "snapshot vs backup".
4. DiseÃ±a el plan 3-2-1 de "tu futuro cliente": memoria en papel de dÃ³nde va cada copia y cada cuÃ¡nto.

## Plataformas gratuitas para practicar

- **restic** (https://restic.net) y **BorgBackup** (https://www.borgbackup.org) â€” documentaciÃ³n impecable
- **Veeam** (https://www.veeam.com) â€” versiÃ³n Community
- **rsync** tutorial: bÃºsqueda en la web *"rsync tutorial backup"*
- Azure/AWS free tier para una copia off-site real en la nube

---

## Checklist de dominio â€” MÃ³dulo 5

- [ ] Explico full/incremental/diferencial y calculo RPO con ellos
- [ ] Elijo RAID correcto segÃºn la carga de trabajo
- [ ] Digo por quÃ© "RAID no es backup" y "snapshot no es backup"
- [ ] DiseÃ±o 3-2-1 (y 1-1 inmutable) para un cliente real
- [ ] Configuro un backup automÃ¡tico real y **lo restauro con Ã©xito**
- [ ] Redacto un runbook DR con RPO/RTO y pasos de restauraciÃ³n
