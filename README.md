# Mi Primera Galaxia Interactiva

**Diseño Web Interactivo — Programación Creativa**

> Proyecto desarrollado como parte de la asignatura **Diseño Web Interactivo**.  
> Estudiante: **Juan Ceballos** · Fecha: 28 de marzo de 2026

---

## Descripción

Experiencia visual interactiva que combina **Tailwind CSS** para la interfaz y **p5.js** para el canvas generativo. Las estrellas/partículas responden al clic y arrastre del mouse, cambian de color y pueden organizarse en diferentes modos de galaxia.

---

## Estructura del Proyecto

```
my-first-interactive-galaxy/
├── p5js_tailwind.md                         ← Guía de clase interactiva
├── mi-galaxia-base.html                     ← Archivo base proporcionado por el docente
├── Actividad_Mi_Primera_Galaxia_Interactiva.md  ← Enunciado de la actividad (4 fases)
├── index.html                               ← Entrega del estudiante (galaxia personalizada)
├── errores-corregidos.txt                   ← Documentación de depuración (Fase 3)
├── Desarrollo_Mi_Primera_Galaxia_Interactiva.md ← Registro de trabajo (Fases 1–4)
└── README.md                                ← Este archivo
```

---

## Flujo de Trabajo

### 1 — Guía de Clase → `p5js_tailwind.html` / `p5js_tailwind.md`

La guía de clase cubre 6 bloques progresivos y demuestra cómo construir una experiencia visual desde cero:

| Bloque | Tema                                                                | Tiempo |
| ------ | ------------------------------------------------------------------- | ------ |
| 0      | Estructura Base HTML + Tailwind (tema Cosmos, glassmorphism)        | 15 min |
| 1      | Canvas p5.js básico (`createCanvas`, `canvas.parent()`, `draw()`)   | 20 min |
| 2      | Sistema de partículas orientado a objetos (clase `Star`)            | 25 min |
| 3      | Interacción con mouse (`mousePressed`, estrellas dinámicas)         | 20 min |
| 4      | Comunicación bidireccional DOM ↔ p5.js (`changeColor()`, `splice`)  | 20 min |
| 5      | Stats en tiempo real + optimizaciones (`frameCount % 10`, fricción) | 20 min |

El archivo `p5js_tailwind.md` es la versión Markdown de la misma guía para consulta offline y consistencia de formato con los demás documentos del proyecto.

### 2 — Archivo Base → `mi-galaxia-base.html`

El docente provee este archivo como punto de partida para la actividad. Implementa todos los bloques de la guía más:

- Card de **Modos de Galaxia**: Nebulosa · Constelación · Pausar · Limpiar
- Función `cambiarModo()` para controlar estados del canvas
- 6 botones de color con indicador activo
- Slider para controlar la cantidad de partículas por clic
- Stats en tiempo real (estrellas, FPS, posición)

### 3 — Actividad → `index.html` + `Desarrollo_Mi_Primera_Galaxia_Interactiva.md`

El estudiante completa 4 fases a partir de `mi-galaxia-base.html`:

| Fase | Actividad                                                      | Duración | Archivo de evidencia                          |
| ---- | -------------------------------------------------------------- | -------- | --------------------------------------------- |
| 1    | Exploración y comprensión del código base                      | 20 min   | `Desarrollo…md` §1                            |
| 2    | Personalización visual (paleta, partículas, modo Supernova)    | 30 min   | `index.html` + `Desarrollo…md` §2             |
| 3    | Depuración de 2 errores controlados                            | 25 min   | `errores-corregidos.txt` + `Desarrollo…md` §3 |
| 4    | Documentación (JSDoc, comentarios de sección, guía de usuario) | 15 min   | `index.html` + `Desarrollo…md` §4             |

---

## Tecnologías

| Tecnología                                | Versión     | Uso                                      |
| ----------------------------------------- | ----------- | ---------------------------------------- |
| [p5.js](https://p5js.org/)                | 1.9.4 (CDN) | Canvas generativo, sistema de partículas |
| [Tailwind CSS](https://tailwindcss.com/)  | 3.x (CDN)   | Interfaz, tema oscuro, glassmorphism     |
| [Google Fonts](https://fonts.google.com/) | —           | Inter (UI) · Fira Code (mono)            |
| HTML5 / JavaScript                        | ES2020      | Sin frameworks adicionales               |

---

## Cómo Usar `index.html`

1. Abre `index.html` directamente en Chrome o Firefox (no requiere servidor)
2. **Modos de galaxia** (card superior):
   - 🌌 **Nebulosa** — agrega 80 estrellas dispersas por el canvas
   - ✨ **Constelación** — agrega 15 estrellas grandes y estáticas
   - 💥 **Supernova** — lanza 50 partículas rápidas desde el centro _(modo personalizado)_
   - ⏸ **Pausar / Reanudar** — congela/reanuda la animación
   - 🧹 **Limpiar** — elimina partículas de colisión, conserva el fondo
3. **Controles de color** (card inferior): selecciona paleta _Llamas Cósmicas_
4. **Clic en el canvas** — lanza una ráfaga de partículas (cantidad ajustable con el slider)
5. **Arrastrar** — genera una estela continua

---

## Personalización "Llamas Cósmicas" (`index.html`)

Cambios realizados respecto al archivo base:

| Elemento                | Original                                  | Personalizado                                |
| ----------------------- | ----------------------------------------- | -------------------------------------------- |
| Tema Tailwind `surface` | `#170d2c` (morado oscuro)                 | `#0c0200` (negro rojizo)                     |
| Tema Tailwind `primary` | `#deb7ff` (lila)                          | `#fb923c` (naranja fuego)                    |
| Paleta de botones       | Primario/Rojo/Teal/Amarillo/Verde/Naranja | Fuego/Coral/Ámbar/Rosa/Magenta/Dorado        |
| Color inicial estrellas | `color(222, 183, 255)`                    | `color(251, 146, 60)`                        |
| Partículas por clic     | 5 (predeterminado)                        | 8 (predeterminado)                           |
| Slider partículas máx.  | 20                                        | 25                                           |
| Velocidad de parpadeo   | `random(0.018, 0.07)`                     | `random(0.03, 0.1)`                          |
| Multiplicador de glow   | ×5                                        | ×6                                           |
| Modo extra              | —                                         | 💥 Supernova (50 partículas desde el centro) |
| Nombres en código       | `stars`, `Star`, `isNew`                  | `estrellas`, `Estrella`, `tipo`              |

---

## Rúbrica (resumen)

| Criterio               | Puntos  |
| ---------------------- | ------- |
| Comprensión del código | 20      |
| Personalización visual | 25      |
| Depuración             | 25      |
| Documentación          | 20      |
| Entrega técnica        | 10      |
| **Total**              | **100** |

---

_Asignatura: Diseño Web Interactivo · Tecnologías: HTML5 · Tailwind CSS v3 · p5.js v1.9.4_
