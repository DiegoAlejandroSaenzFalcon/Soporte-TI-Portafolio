# 0406 · Módulo 6: Proyecto Final — Casos Prácticos de Infraestructura

> Curso 04 · Módulo 6 de 6 · Temas: resolver casos reales integrando todo lo aprendido

---

## Objetivos de este módulo

- [ ] Analizar un caso de infraestructura completo y elegir la solución
- [ ] Comunicar decisiones técnicas con justificación
- [ ] Entregar documentación de nivel profesional
- [ ] Presentar el caso como en una entrevista técnica

---

## Caso 1: Pequeña oficina (20 empleados) — el "pan de cada día"

**Escenario**: oficina de seguros con 20 personas. Todo en equipos sueltos, sin servidor. Quejas: los archivos "se pierden", el correo llega tarde, no hay copias de seguridad.

**Análisis y propuesta** (piénsalo antes de leer la solución):

| Problema detectado | Solución propuesta |
|--------------------|--------------------|
| Archivos dispersos sin copias | NAS/pequeño servidor de archivos + backups diarios (3-2-1) |
| Sin autenticación centralizada | Microsoft 365 + Entra ID (cuentas, MFA, correo) |
| Sin políticas de seguridad | GPO o políticas de Entra: contraseñas fuertes, cifrado BitLocker |
| Sin monitoreo ni documentación | Runbooks + checklists mensuales + monitoreo del NAS |

**Prioridades en orden**: 1) backups AHORA → 2) identidades (correo, MFA) → 3) políticas → 4) documentación.

---

## Caso 2: Empresa mediana (5 sucursales) — escalar bien

**Escenario**: 5 oficinas conectadas por VPN a la sede central. Un servidor físico en sede central hace todo (web, correo, archivos, directorio) y "siempre se cae". Los usuarios de las sucursales sufren latencia.

**Análisis**:

| Problema | Solución |
|----------|----------|
| Un solo servidor hace todo (SPOF) | Separar roles: 1 servidor archivos, 1 directorio/DC, 1 aplicaciones; RAID 1/10 |
| Sin tolerancia a fallos | Segundo DC + backup y replicación con el segundo sitio |
| Latencia en sucursales | **Replicación de archivos por sitio** (DFS o similar) o mover servicios a la nube |
| Crecimiento de datos | Política de retención + archivado + presupuesto de almacenamiento |
| Sin plan de desastre | DR runbook con RPO 24 h / RTO 24 h y prueba anual |

**Propuesta final**: nube híbrida (correo y colaboración en cloud; archivos críticos replicados; copia inmutable off-site).

---

## Caso 3: Migración (escenario de entrevista típico)

**Escenario**: la empresa quiere pasar de correo local a Microsoft 365, de archivos locales a SharePoint/OneDrive y de cuentas sueltas a Entra ID. Vendes el plan.

**Plan de migración en fases** (formato profesional):

1. **Inventario**: usuarios, buzones, tamaños, dependencias de apps.
2. **Prueba piloto** con 5 usuarios y correo "actual".
3. **Migración por lotes** (25% por semana), verificando buzones y archivos.
4. **Corte** definitivo, redirección de dominios (DNS/MX con TTL bajo antes).
5. **Rollback plan**: cómo revertir si algo falla.
6. **Capacitación** de usuarios con guías cortas.
7. **Post-cambio**: monitorear por 2 semanas, resolver cola residual, documentar.

**Justificación técnica**: redundancia del proveedor, MFA incluido, licencias, ahorro en administración, cumplimiento (retention policies).

---

## Cómo entregar un caso (checklist profesional)

| Punto | Detalle |
|-------|---------|
| **Entender primero** | Releer el escenario, anotar datos duros (usuarios, sitios, servicios) |
| **Priorizar** | Qué resolver primero (¿hay riesgo de pérdida de datos? → backups primero) |
| **Proponer y justificar** | Cada elección con "por qué" (no solo "qué") |
| **Presupuestar conceptos** | Costos aproximados (hardware vs SaaS) en rangos |
| **Comunicar simple** | Explicarlo como si el jefe no fuera técnico |
| **Entregar documentación** | Diagrama + runbooks + plan DR + cronograma |

---

## Práctica final del curso

1. Diseña la solución completa del Caso 1 con diagrama (app.diagrams.net) y runbook de backups.
2. Redacta el plan de migración del Caso 3 en 1 página profesional.
3. Graba/repasa tu explicación del Caso 2 en voz alta (2 min) — esto se parece a una entrevista real.
4. Ármalo en tu VM: levanta el mini-servidor del Caso 1 (fileserver Samba + rsync backup).

## Recursos de apoyo

- **app.diagrams.net** para diagramas profesionales
- Documentación oficial de Microsoft 365 (https://learn.microsoft.com) — planes de migración
- **Cisco NetAcad** para conceptos de red de sucursal
- Buscas en la web: *"IT infrastructure case study small office"* para más casos

---

## Checklist de dominio — Módulo 6

- [ ] Analizo un caso y entrego prioridades justificadas
- [ ] Propongo soluciones con presupuesto conceptual
- [ ] Vendo un plan de migración en fases con rollback
- [ ] Comunico decisiones técnicas a una audiencia no técnica
- [ ] Entrego diagrama + runbooks + plan DR como entregables
- [ ] Podría defender el caso en una entrevista de sysadmin junior

---

## Fin del Curso 04 — Siguiente paso
Completa el examen del curso (opcional) y continúa con el último: **Curso 05 · Seguridad Informática** →