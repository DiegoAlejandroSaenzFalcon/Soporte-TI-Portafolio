# GH-05 · Módulo 5: Tu cuenta, seguridad y buenas prácticas

> Guía GitHub · Módulo 5 de 6 · Temas: crear cuenta, autenticación en dos pasos, qué NUNCA subir, repos privados para datos sensibles, buenos mensajes de commit

---

## Objetivos de este módulo

- [ ] Crear mi cuenta gratuita y activar la verificación en dos pasos
- [ ] Listar las 5 cosas que NUNCA van a un repositorio
- [ ] Elegir público/privado según el contenido
- [ ] Escribir mensajes de commit profesionales

---

## 1. Tu cuenta gratuita (el primer paso del creador)

Crea tu cuenta en la página de inicio de GitHub (nombre de usuario profesional, correo real, contraseña fuerte). Consejos:

- El **nombre de usuario** es tu marca pública: coherente con el CV (`diegosaenz` o similar).
- Activa **verificación en dos pasos** (2FA): en Configuración → Password and authentication. Es la diferencia entre "robable" y "protegida".
- No compartas tu cuenta ni tus contraseñas con nadie.

**Auto-explicación**: explica en voz alta por qué un repositorio con tus datos NO debe depender solo de una contraseña.

## 2. Las 5 cosas que NUNCA subes (a ningún repositorio)

| Prohibido | Ejemplo | Consecuencia si se publica |
|-----------|---------|----------------------------|
| **Contraseñas y tokens** | claves de correo, API keys, tokens | Alguien entra como tú |
| **Datos personales sensibles** | DNI, direcciones, teléfonos de terceros | Robo de identidad legal |
| **Datos de clientes/empresa** | nóminas, bases de datos | Problemas legales graves |
| **Certificados/llaves privadas** | archivos `.pem`, `.key` | Acceso a sistemas privados |
| **Información embarazosa o falsa** | mentiras en CV, chismes | Daño de reputación permanente |

**Las "público" se ven en el mundo**: antes de hacer clic en publicar, aplica la prueba de los 10 segundos: *"¿me molestaría que un reclutador me lo preguntara en una entrevista?"*.

## 3. Público vs privado según el contenido (matriz de decisión)

| Contenido | Recomendación |
|-----------|---------------|
| Guías de estudio, portafolio, proyectos que demuestran trabajo | **Público** (es tu escaparate) |
| Proyectos con datos de clientes, ideas en desarrollo muy temprano | **Privado** (puedes hacerlo público después) |
| Trabajo para terceros | Privado casi siempre (según contrato) |

**Una decisión inteligente**: los proyectos crecen y cambian de visibilidad. Un proyecto privado en fase 1 puede pasar a público cuando demuestre calidad — es lo natural en todos los perfiles profesionales.

## 4. Mensajes de commit profesionales (tu firma en el historial)

El mensaje de commit es lo que leerá cualquier persona que revise la historia. Escritura profesional:

| Mal mensaje | Bien | Por qué |
|-------------|------|---------|
| "cambios" | "Corrige tildes del módulo 0102" | Explica QUÉ exactamente |
| "arreglo error" | "Arregla la ruta del diagrama en 0202" | Ubica el cambio |
| "x" | "Añade ejemplos resueltos al curso 06" | Describe el beneficio |

**Formato corto profesional**: `[Verbo en presente] + [qué] + [dónde opcional]` — como los que verás en el historial de este repositorio.

## 5. Ejercicio guiado

1. Crea tu cuenta (o revisa la tuya): activa 2FA hoy mismo.
2. Revisa la lista "5 cosas que nunca se suben" y marca las que aplican a tus archivos actuales.
3. Decide la visibilidad de 3 proyectos futuros (guía, Soluciona, un juego) usando la matriz.
4. Escribe 3 mensajes de commit para cambios hipotéticos de tu guía local.
5. Auto-explicación: "¿por qué la 2FA es obligatoria para quien guarda proyectos en la nube?"

## 6. Checklist de dominio (sin mirar el módulo)

- [ ] Mi cuenta tiene 2FA activada
- [ ] Enumero 5 cosas que nunca se suben
- [ ] Elijo visibilidad con criterio según contenido
- [ ] Escribo mensajes de commit con verbo + qué + dónde
- [ ] Explico la prueba de los 10 segundos

---

**Siguiente módulo**: [GH-06 — Proyecto: tu primer repositorio](./gh-06-modulo-6-proyecto-primer-repositorio.md)