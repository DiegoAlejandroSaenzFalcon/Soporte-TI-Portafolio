# Guía de GitHub para principiantes (aplicada a tu repositorio)

Esta guía te enseña a **navegar tu propio proyecto en GitHub** sin saber nada de git. Escríbela, léela dos veces y nunca más te perderás. Todo lo que necesitas saber para estudiar tu guía de soporte TI está aquí.

---

## 1. ¿Qué es GitHub, en una frase?

Una **biblioteca digital** donde tus documentos viven esquina por esquina con su historial de versiones. Tú la usas para leer y mostrar; nosotros (o tú con copilot) la usamos para escribir.

## 2. Las 3 zonas de tu repositorio (memoriza esto)

| Zona | Cómo se ve | Para qué sirve |
|------|------------|----------------|
| **Pestaña Code (inicio)** | Listado de carpetas y archivos | Navegar y leer documentos — **la única zona que necesitas** |
| **Pestaña Commits** | Lista de "guardados" con fecha | Ver el historial de cambios; no se lee para estudiar |
| **Vista de un commit** | Texto rojo tachado + texto verde | Comparar versiones; los tachados son líneas *eliminadas* — ¡no son tu contenido! |

> **Regla de oro**: para estudiar, usa siempre la **pestaña Code**. Los commits solo se miran si quieres ver "qué cambió".

## 3. Cómo navegar la biblioteca (5 gestos)

1. **Entrar a una carpeta**: clic en su nombre (ej. `guia-google-it-support`).
2. **Entrar a un archivo**: clic en su nombre. Los archivos `.md` se abren **renderizados** (bonitos, con tablas y diagramas), no como código.
3. **Volver un nivel**: clic en el **breadcrumb** de arriba (la ruta muestra: `Soporte-TI-Portafolio > guia-google-it-support > curso-02...`). Haz clic en cualquier parte de esa ruta para subir.
4. **Ver imágenes/diagramas**: clic en un archivo `.svg` → se muestra el dibujo; para volver: flecha atrás o breadcrumb.
5. **Descargar todo el proyecto**: botón verde **"Code"** → **"Download ZIP"**. Esa descarga es una copia exacta para tus apuntes (válida también sin sesión).

## 4. Por qué las carpetas "se ven desordenadas" (y cómo leerlas)

GitHub ordena **alfabéticamente**, no por número:

- `00-vision-general.md` va primero por el "0" (es la introducción del curso, no el módulo 0).
- El diagrama sale *antes* que su módulo (`0104-diagrama...` antes que `0104-modulo...`).
- `README.md` queda al final de la lista.

**Orden de lectura correcto en cada curso**:
`README.md` (portada del curso) → `00-vision-general.md` (vistazo) → módulo 1 → módulo 2 → … → módulo 6.

## 5. El patrón de lectura que te recomiendo

1. Abre la raíz → `README.md` (mapa completo).
2. Elige un curso → entra a `curso-XX` → lee su `README.md`.
3. Abre `00-vision-general.md` para el plan del curso.
4. Estudia módulo por módulo, con su diagrama.
5. Reporta tus avances marcando las casillas `- [ ]` de los objetivos.

## 6. Preguntas frecuentes rápidas

| Pregunta | Respuesta |
|----------|-----------|
| ¿Necesito cuenta para leer? | **No** — todo es público (prueba en modo incógnito) |
| ¿Necesito saber git para estudiar? | No, navegas como en Drive |
| ¿Dónde están "los documentos"? | Todos los `.md` dentro de `guia-google-it-support/` |
| ¿Puedo romper algo navegando? | No. Leer no toca nada |
| ¿Y si quiero aprender a *editar*? | Eso es el siguiente nivel (branch + pull request); lo haremos cuando quieras |
| ¿Se puede ver como página web estética? | Sí: **GitHub Pages** lo convierte en sitio web — es el siguiente proyecto que podemos montar |

## 7. El test de autoevaluación (5 preguntas)

1. ¿Qué pestaña debo usar siempre para estudiar? _(Code)_
2. ¿Qué significa el texto tachado en un commit? _(líneas eliminadas en esa versión)_
3. ¿Dónde está el módulo 6 de redes? _(0206-modulo-6-troubleshooting-y-futuro-de-las-redes.md)_
4. ¿Qué aparces primero en una carpeta de curso? _(00-vision-general.md)_
5. ¿Cómo bajo todo el proyecto a mi PC? _(Code → Download ZIP)_

Aprobado si respondes las 5 sin mirar. Ese es el nivel 3 de la rúbrica.