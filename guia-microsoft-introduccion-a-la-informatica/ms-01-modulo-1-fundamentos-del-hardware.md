# MS-01 · Módulo 1: Fundamentos del hardware y la IA

> Guía Microsoft · Módulo 1 de 6 · Temas: CPU, memoria, almacenamiento, periféricos, GPU y el hardware detrás de la IA generativa

---

## Objetivos de este módulo

- [ ] Identificar los componentes clave de un sistema (CPU, RAM, almacenamiento, periféricos)
- [ ] Explicar cómo interactúan esos componentes (el flujo de un clic)
- [ ] Entender por qué la GPU es la reina de la IA generativa
- [ ] Calcular el "paso a paso" de un programa: hardware + software

---

## Diagramas de esta sección

| Diagrama | Qué te enseña |
|----------|---------------|
| [La computadora es una cocina](./ms-01-diagrama-la-computadora-es-una-cocina.svg) | El rol de cada componente y el flujo completo de un clic |

---

## 1. La computadora como una cocina (analogía maestra)

| Componente | En la cocina | En la PC |
|------------|--------------|----------|
| **CPU** | El chef (decide y ejecuta cada movimiento) | El procesador: ejecuta instrucciones |
| **RAM** | La mesa de trabajo (ingredientes a mano) | Memoria rápida y temporal (se borra al apagar) |
| **Disco** | La despensa (todo almacenado) | Almacenamiento permanente (SSD/HDD) |
| **GPU** | El ayudante especialista en freír 100 papas a la vez | Procesador de gráficos/paralelo masivo |
| **Placa base** | La cocina entera (todo conectado) | Conecta todos los componentes |
| **Periféricos** | Utensilios y comensales | Entrada (teclado, mouse) y salida (pantalla, impresora) |

**El flujo de un clic** (auto-explicación en 4 pasos):
1. El **mouse/relevo** envía la señal → la **CPU** recibe la interrupción.
2. La CPU busca el programa en el **disco** y lo trae a la **RAM** (mesa).
3. La CPU ejecuta las instrucciones del programa; la **GPU** se encarga si hay gráficos.
4. El resultado viaja al **monitor** (salida).

Recuerda: es el mismo flujo del modelo de 5 capas de redes — capas que hablan entre sí, cada una con su trabajo.

## 2. CPU: el chef con límites

La CPU ejecuta **instrucciones** (operaciones básicas: sumar, comparar, mover). Un programa es una receta enorme de estas operaciones.

| Concepto | Significado | Analogía |
|----------|-------------|----------|
| **Núcleos (cores)** | Cuántas recetas en paralelo | Chefs simultáneos |
| **Frecuencia (GHz)** | Cuántas instrucciones por segundo | Velocidad de cada chef |
| **Caché** | Memoria ultra-rápida interna | Ingredientes en el bolsillo del chef |
| **Arquitectura 32/64 bits** | Tamaño de los "platos" que maneja | Ancho de la vajilla |

**Cálculo sencillo**: una CPU de 4 núcleos a 3 GHz ≈ 12 mil millones de "pasos de chef" por segundo. Cada clic que ves consume cientos de millones de pasos — por eso tu PC hace "cosas imposibles" sin esfuerzo aparente.

**Ejercicio guiado (Windows y macOS)**: abre el administrador de tareas (Ctrl+Shift+Esc) o el monitor de actividad. En la pestaña "Rendimiento" identifica: uso de CPU y de memoria, y toma nota de si el disco está al tope. Diagnóstico aplicado del módulo.

## 3. RAM vs Almacenamiento (la confusión nº1)

| | RAM | Disco (SSD/HDD) |
|--|-----|-----------------|
| Velocidad | Extremadamente rápida | Lenta en comparación (SSD mucho mejor que HDD) |
| Volatilidad | Se borra al apagar | Permanente |
| Precio | Caro por GB | Barato por GB |
| Tamaño típico hoy | 8-32 GB | 256 GB - 2 TB |
| Uso | Programas en ejecución | Todo el sistema y tus archivos |

**Regla práctica**: si la PC "va lenta con muchos programas abiertos" → falta RAM, no disco. Si "tarda en arrancar y abrir programas" → disco lento (HDD) o casi lleno → SSD o liberación.

> **Método científico aplicado**: ante una PC lenta nunca "compra más RAM" a ciegas. Observa (administrador de tareas) → hipótesis (¿memoria al 95% o disco al 100%?) → experimento (cierra pestañas/programas y mide) → conclusión.

## 4. GPU: el hardware que impulsiona la IA generativa

La IA generativa (texto, imágenes, voz) se entrena con **redes neuronales**: miles de millones de multiplicaciones y sumas en paralelo. La CPU hace pocas cosas muy rápido; la **GPU hace millones de cosas simples al mismo tiempo** — exactamente lo que necesita una red neuronal.

| Tarea | CPU (chef) | GPU (1000 ayudantes) |
|-------|-----------|----------------------|
| Editar hoja de cálculo | Rápido | Desperdicio (no paralelizable) |
| Videojuego con gráficos | Lento | Perfecta |
| Entrenar/ejecutar un modelo de IA | Muy lento | Hecha para esto |

Datos importantes para hablar con criterio:
- Las GPU modernas tienen **decenas de miles de núcleos** especializados.
- Un modelo de IA grande se entrena en **granjas de GPU** durante semanas.
- En tu celular o PC hay **aceleradores de IA** cada vez más comunes (NPU).

**Auto-explicación**: explica en voz alta por qué una red neuronal (muchas operaciones simples en paralelo) y una GPU (muchos núcleos simples) son "alma gemela".

## 5. Periféricos y almacenamiento

| Periférico | Tipo | Ejemplos |
|------------|------|----------|
| Entrada | Envían datos a la PC | Teclado, mouse, micrófono, cámara, escáner |
| Salida | Reciben datos de la PC | Monitor, impresora, parlantes |
| Mixto | Ambos | Pantalla táctil, impresora multifunción |

**Almacenamiento moderno** (debes elegirlo con criterio):

| Tipo | Ventaja | Inconveniente | Uso típico |
|------|---------|---------------|------------|
| **SSD NVMe** | Rápido (x10 vs HDD) | Costo por GB | Sistema y programas |
| **SSD SATA** | Rápido y estable | Más lento que NVMe | Dato frecuente |
| **HDD** | Barato por GB, gran capacidad | Lento, frágil | Archivos grandes, backups |
| **Nube** | Accesible desde todo lado, redundante | Requiere internet, costo mensual | Cooperación y backup |

**Regla 3-2-1** (recordatorio del curso de backups): 3 copias, 2 medios distintos, 1 fuera de sitio.

## 6. Ejercicios

1. **Ejemplo resuelto desvanecido**: te damos la tabla completa de "¿falta RAM o disco?" (ej. caso A: programas lentos con disco al 10% → caso B: arranque lento con disco al 98%). Resuelve el caso C tú solo: "el videojuego se traba con 2 GB libres de RAM y GPU al 60%".
2. **Laboratorio casero**: monitorea tu PC durante 1 hora de uso real. Registra: % CPU, % RAM, % disco en 3 momentos. Presenta una conclusión con hipótesis (¿qué faltaría para que fuera más rápida?).
3. **Taller de spec**: con 3 presupuestos dados (bajo/medio/alto), elige la PC para un estudiante de TI, un diseñador y un jugador. Justifica cada elección con los conceptos del módulo (Bloom: evaluar).
4. **Auto-explicación**: graba un audio de 1 min explicando "qué pasa dentro del clic" sin mirar apuntes.

## 7. Checklist de dominio (sin mirar el módulo)

- [ ] Explico la analogía cocina: CPU/RAM/disco/GPU
- [ ] Describo el flujo de un clic en 4 pasos
- [ ] Diagnostico "falta RAM" vs "disco lento" con evidencia
- [ ] Explico por qué la GPU es clave para la IA generativa
- [ ] Elijo entre SSD/HDD/nube según el caso

---

**Siguiente módulo**: [MS-02 — Sistemas operativos](./ms-02-modulo-2-sistemas-operativos.md)