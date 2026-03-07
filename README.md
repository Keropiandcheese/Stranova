# Encuesta de Evento — Stranova

Página web para que alumnos respondan una encuesta de evaluación de un evento. Los datos se envían directamente a una base de datos en **Supabase**.

---

## ¿Qué hace?

1. El alumno ingresa su **nombre completo** y **grupo**
2. Se le presentan **12 preguntas** de evaluación del evento
3. Al enviar, los datos se guardan en Supabase
4. Se muestra una pantalla de confirmación personalizada con su nombre

---

## Estructura del formulario

| Paso | Descripción |
|------|-------------|
| **Paso 1** | Formulario de datos: nombre y grupo |
| **Paso 2** | 12 preguntas de evaluación |
| **Paso 3** | Pantalla de confirmación |

### Preguntas

- **P1 – P10** → Preguntas de opción múltiple (botones seleccionables)
- **P11** → Texto libre: *¿Qué fue lo que más te gustó del evento?*
- **P12** → Texto libre: *¿Qué aspectos consideras que pueden mejorar?*

---

## Base de datos (Supabase)

La tabla utilizada es `asistencia`. Requiere las siguientes columnas:

| Columna | Tipo | Notas |
|---------|------|-------|
| `nombre` | `text` | **Primary Key** — evita registros duplicados |
| `grupo` | `text` | |
| `p1` – `p10` | `text` | Respuestas de opción múltiple |
| `p11` | `text` | Respuesta abierta |
| `p12` | `text` | Respuesta abierta |

---

## Validaciones incluidas

- **Campos vacíos** — no avanza al paso 2 si falta nombre o grupo
- **Preguntas sin contestar** — alerta `"Por favor, contesta la pregunta X"` con scroll automático a la pregunta faltante (aplica para las 12 preguntas)
- **Nombre duplicado** — si el nombre ya existe en la base de datos, muestra `"Ya respondiste esta encuesta"`
- **Cookie de sesión** — guarda el nombre del alumno en un cookie de 7 días para pre-rellenarlo si regresa

---

## Archivos

```
index.html   → Página principal (formulario + lógica + modelos 3D)
style.css    → Estilos de la página
```

---

## Configuración

Las credenciales de Supabase están definidas al inicio del script en `index.html`:

```js
const SB_URL = "https://<tu-proyecto>.supabase.co";
const SB_KEY = "<tu-anon-key>";
```
---

## Tecnologías

- HTML / CSS / JavaScript vanilla
- [Supabase](https://supabase.com) — base de datos y API REST
- [Model Viewer](https://modelviewer.dev) — visualización de modelos 3D `.glb`