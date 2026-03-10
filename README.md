# 📋 Encuesta de Evento — Katchi × Pálida | Stranova

Página web interactiva para que alumnos evalúen una conferencia de moda streetwear. Incluye modelos 3D giratorios, formulario de encuesta en pasos, envío de datos a Supabase y un panel de resultados para administradores.

---

## ¿Qué hace la página?

### Vista del alumno

La página se divide en dos secciones:

**Sección superior — Modelos 3D**
Muestra dos modelos `.glb` animados (gorra y vestido) que rotan automáticamente. El usuario puede girarlos con el dedo o el mouse arrastrando sobre las zonas de toque. En el centro aparecen los logos de Katchi y Pálida con enlace a sus Instagrams, y el logo de la UDL abajo.

**Sección inferior — Formulario en 3 pasos**

```
Paso 1 → Ingresa nombre y grupo
Paso 2 → Responde 12 preguntas de evaluación
Paso 3 → Pantalla de confirmación personalizada
```

---

## Flujo completo del usuario

```
┌─────────────────────────────────┐
│  Escribe nombre + grupo         │
│  y presiona REGISTRAR           │
└────────────┬────────────────────┘
             │
             ▼
┌─────────────────────────────────┐
│  ¡Hola, [nombre]!               │
│  Aparecen las 12 preguntas      │
│                                 │
│  P1–P10 → botones de opción     │
│  P11–P12 → campos de texto      │
└────────────┬────────────────────┘
             │
             ▼
┌─────────────────────────────────┐
│  Validación antes de enviar:    │
│  • ¿Respondiste todas?          │
│  • ¿Los textos tienen algo?     │
│  • ¿El nombre ya existe?        │
└────────────┬────────────────────┘
             │
             ▼
┌─────────────────────────────────┐
│  POST a Supabase                │
│  Tabla: asistencia              │
│  Columnas: nombre, grupo,       │
│            p1 … p12             │
└────────────┬────────────────────┘
             │
             ▼
┌─────────────────────────────────┐
│  ¡Gracias, [nombre]!            │
│  Scroll automático a esta       │
│  pantalla de confirmación       │
└─────────────────────────────────┘
```


---

## Validaciones

- **Campos vacíos** — no avanza si falta nombre o grupo
- **Preguntas sin contestar** — muestra `"Por favor, contesta la pregunta X"` y hace scroll automático hasta ella
- **Textos vacíos** — valida que P11 y P12 tengan al menos algo escrito
- **Nombre duplicado** — si el nombre ya existe en Supabase (es Primary Key), muestra `"Ya respondiste esta encuesta"`
- **Cookie de sesión** — guarda el nombre 7 días para pre-rellenarlo si el alumno regresa

---

## Panel de administrador

Se accede poniendo `admin` en nombre y `7001` en grupo.

### ¿Qué muestra?

**Gráficas de pastel (P1–P10)**
Una gráfica por cada pregunta de opción múltiple. Las opciones aparecen en el mismo orden que en el formulario, con colores fijos:

| Color | Significa |
|-------|-----------|
| 🟡 Amarillo | Sí / Excelente / Mucho / Muy satisfecho |
| 🟠 Naranja | Opciones intermedias |
| 🔵 Azul | Opciones intermedias |
| 🔴 Rojo | No / Mala / Insatisfecho |

**Acordeones de texto (P11 y P12)**
Cada pregunta es una cajita colapsable. Al abrirla muestra todas las respuestas con el nombre y grupo de cada alumno. Tiene buscador para filtrar por nombre.

---

## Base de datos — Supabase

**Tabla:** `asistencia`

| Columna | Tipo | Notas |
|---------|------|-------|
| `nombre` | `text` | **Primary Key** |
| `grupo` | `text` | |
| `p1` – `p10` | `text` | Respuestas de opción múltiple |
| `p11` | `text` | Respuesta abierta |
| `p12` | `text` | Respuesta abierta |

---

## Archivos del proyecto

```
/
├── index.html              → Página principal
├── style.css               → Estilos globales
├── assets/
│   ├── img/
│   │   ├── katchi.png      → Logo Katchi
│   │   ├── palida.png      → Logo Pálida
│   │   └── udl.png         → Logo universidad
│   └── obj/
│       ├── gorra.glb       → Modelo 3D gorra
│       └── dress.glb       → Modelo 3D vestido
└── stranova/
    └── Stranova.jpg        → Banner footer
```

---
