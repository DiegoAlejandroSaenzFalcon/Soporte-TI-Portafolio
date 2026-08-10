# MS-05 · Módulo 5: Aplicaciones de negocio

> Guía Microsoft · Módulo 5 de 6 · Temas: ERP, BI, productividad, ecosistemas cloud y el "back office" digital de la empresa

---

## Objetivos de este módulo

- [ ] Explicar qué es un ERP y por qué las empresas no viven sin él
- [ ] Entender qué hace la inteligencia de negocio (BI) con los datos
- [ ] Situar la productividad moderna en el ecosistema cloud
- [ ] Conectar hardware, SO, seguridad y negocio en un caso integrador

---

## 1. ERP: el sistema nervioso de la empresa

**ERP** (Enterprise Resource Planning) = un único sistema que integra todas las áreas: ventas, compras, inventario, finanzas, RH, producción.

| Área | Antes (sistemas separados) | Con ERP (integrado) |
|------|----------------------------|---------------------|
| Venta | La vendedora pide el precio a otro departamento | El ERP ya tiene el precio e inventario |
| Inventario | Se enteran de la falta al final de mes | El ERP descuenta al instante y avisa reposición |
| Finanzas | Reconciliar 4 reportes que no cuadran | Un solo registro para todo |
| Producción | "¿Hay materia prima?" — telefono y espera | Disponibilidad en pantalla, en tiempo real |

**Analogía**: el ERP es el **sistema circulatorio** del negocio — si un área se atasca, todas lo sienten. Su costo (dinero y migración) es alto, por eso las empresas lo eligen con matrices muy parecidas al método científico del módulo 3.

**Ejemplo resuelto**: una ferretería crece a 5 sucursales y sigue en Excel → errores de inventario, 2 veces la misma factura, desorden. Con ERP: un solo inventario, venta cruza el depósito al instante. La lección: la tecnología crece con el negocio, no por capricho.

## 2. BI: convertir datos en decisiones

**BI** (Business Intelligence) = herramientas que convierten montones de datos en **informes y dashboards** para decidir.

El flujo del dato en la empresa moderna:

```
Datos crudos (ventas, clima, tráfico, web)
   → almacenes de datos (data warehouse)
   → herramientas BI (Power BI, Tableau o similares)
   → dashboards y alertas
   → decisiones (inventario, marketing, precios)
```

**En lenguaje llano**: no es "tener datos", es **ver la foto de tu negocio** a tiempo. Un dashboard de la ferretería: ventas por sucursal, productos que más rotan, horas pico, ticket promedio. Con eso el dueño decide dónde invertir el fin de semana promocional.

**Regla de oro del BI**: la mejor herramienta del mundo no arregla datos sucios (basura entra, basura sale). La calidad del dato se protege desde la tríada CIA del módulo anterior (integridad).

## 3. Productividad y ecosistemas cloud

Las aplicaciones de productividad modernas (correo, documentos, hojas, calendario, chats) viven en el cloud:

| Ventaja cloud | En la oficina | Para el usuario |
|---------------|---------------|-----------------|
| Colaboración en vivo | Varios editan el mismo documento al tiempo | Sin versiones "final_v3_YA.docx" |
| Acceso desde cualquier dispositivo | Escritorio, tablet, celular | Trabajo híbrido real |
| Escalabilidad | Crece sin comprar servidores | Se agrega usuario sin drama |
| Seguridad centralizada | Proveedor aplica los parches y backups | Tú te concentras en el trabajo |
| Costo | Pago por uso predecible | Sin mantenimiento propio |

**El modelo "SaaS"**: el software como servicio — ya no compras licencias e instalas: te suscribes y listo. Es la capa superior del modelo (IaaS infraestructura, PaaS plataforma, SaaS aplicación) que viste en el curso de redes — aquí se cierra el círculo: **hardware (M1) → red y cloud (M3) → seguridad (M4) → negocio (M5)**.

## 4. Ejercicio integrador (el primer ensayo del proyecto final)

**Caso**: "Restaurante de 3 locales quiere digitalizarse". Con lo aprendido en M1-M5, responde:

1. ¿Qué hardware necesita cada local y el centro? (M1-M3)
2. ¿Qué papel juega la nube? ¿Y la seguridad de los pagos? (M3-M4)
3. ¿Qué sistema (ERP/BI) resolvería su inventario y sus decisiones? (M5)
4. ¿Qué backup y plan de continuidad le propones? (M3-M4)

**Prompt sugerido para contrastar** (y verificar todo): *"Actúa como consultor de TI para una pyme. Revisa mi propuesta de digitalización de un restaurante de 3 locales: dime qué falta, qué es excesivo y qué preguntas me haría el dueño."*

## 5. Ejercicios

1. **Ejemplo resuelto desvanecido**: proyecto completo de "libería con 2 tiendas" (ERP ligero, BI básico, nube). Ahora haz el de "gimnasio con membresías".
2. **Laboratorio**: abre un dashboard con datos que tienes a mano (gastos del mes en una hoja de cálculo) y crea 2 gráficos que te ayuden a decidir algo real. Documéntalo.
3. **Análisis**: elige 2 ERPs populares y compáralos (público, precio, fortaleza/industria, nube/on-prem). Justifica cuál elegirías para una pyme de retail.
4. **Auto-explicación**: explica el flujo "datos → BI → decisión" con el ejemplo del restaurante, sin apuntes.

## 6. Checklist de dominio (sin mirar el módulo)

- [ ] Explico qué es un ERP con la analogía del sistema circulatorio
- [ ] Describo el flujo del dato hasta la decisión (BI)
- [ ] Defiendo 3 ventajas del cloud para la productividad
- [ ] Conecto hardware → cloud → seguridad → negocio en un caso
- [ ] Expliqué por qué la calidad del dato precede a la herramienta

---

**Siguiente módulo**: [MS-06 — Proyecto final: arquitecto de soluciones](./ms-06-modulo-6-proyecto-final.md)