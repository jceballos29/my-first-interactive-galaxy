# Desarrollo de Actividad: Mi Primera Galaxia Interactiva

**Estudiante :** Juan Ceballos  
**Fecha :** 28 de marzo de 2026  
**Asignatura :** Diseño Web Interactivo  
**Archivo entregado :** `index.html`

---

## ✅ FASE 1: Exploración y Comprensión (20 min)

### A. Preguntas sobre HTML (Tailwind)

**¿Qué hace la clase `"fixed inset-0 -z-10"`?**  
Posiciona el elemento como `fixed` (fijo respecto a la ventana, no al documento).  
`inset-0` aplica `top: 0; right: 0; bottom: 0; left: 0`, haciendo que el elemento cubra toda la pantalla.  
`-z-10` asigna `z-index: -10`, colocándolo detrás de todos los demás elementos.  
→ Resultado: el canvas de p5.js actúa como fondo animado sin tapar la UI.

**¿Para qué sirve `onclick="cambiarModo('nebulosa')"`?**  
Es un manejador de evento _inline_ que, al hacer clic en el botón, llama la función JavaScript `cambiarModo()` y le pasa el string `'nebulosa'` como argumento.  
Permite que el HTML controle el comportamiento del canvas de p5.js a través de variables globales compartidas: comunicación DOM → p5.js.

**¿Qué significa `"backdrop-blur-xl"` visualmente?**  
Aplica un desenfoque gaussiano grande (**blur**) al área visible detrás del elemento, creando el efecto _glassmorphism_: el fondo se ve difuminado como si el elemento fuera un vidrio esmerilado.  
Requiere que el elemento tenga fondo semitransparente para que el blur sea visible.

---

### B. Preguntas sobre JavaScript (p5.js)

**¿Cuándo se ejecuta `setup()` vs `draw()`?**  
`setup()` se ejecuta **una sola vez** al cargar el sketch; sirve para inicializar variables, crear el canvas y definir el estado inicial.  
`draw()` se ejecuta en **bucle continuo** a ~60 fps mientras la animación esté activa. Todo lo que necesite actualizarse frame a frame (movimiento, color, partículas) va aquí.

**¿Qué representa la clase `Estrella`?**  
Cada instancia de `Estrella` representa una partícula/punto luminoso individual. Encapsula en un solo objeto: posición (`x`, `y`), velocidad (`vx`, `vy`), ciclo de vida (`vida`), tamaño (`tamano`), color (`col`), tipo (`'normal'`/`'colision'`) y propiedades de parpadeo (`velocidadBrillo`, `offsetBrillo`). Cada estrella es autónoma y responsable de su propio ciclo de vida.

**¿Qué diferencia hay entre tipo `'normal'` y tipo `'colision'`?**

| Propiedad      | `'normal'`                       | `'colision'`                              |
| -------------- | -------------------------------- | ----------------------------------------- |
| Origen         | Posición aleatoria en pantalla   | Posición del cursor                       |
| Velocidad      | `vx = 0`, `vy = 0` (no se mueve) | `vx` y `vy` aleatorios                    |
| Vida           | `-1` (inmortal)                  | `255` → decrementa a 0                    |
| `estaMuerta()` | Siempre `false`                  | `true` cuando `vida ≤ 0`                  |
| Efecto visual  | Parpadeo sinusoidal              | Movimiento con fricción + desvanecimiento |

---

### C. Predicciones (antes de probar)

| #   | Cambio propuesto                     | Mi predicción                                                     | ¿Se cumplió? |
| --- | ------------------------------------ | ----------------------------------------------------------------- | ------------ |
| 1   | `80` → `200` en modo 'nebulosa'      | Aparecerían 200 estrellas al activar Nebulosa; pantalla más llena | ✅ Correcto  |
| 2   | `this.vida -= 3` → `this.vida -= 10` | Las colisiones desaparecerían ~3× más rápido                      | ✅ Correcto  |
| 3   | `random(-4, 4)` → `random(-10, 10)`  | Las partículas saldrían con mucha más dispersión y velocidad      | ✅ Correcto  |

---

## ✅ FASE 2: Personalización Visual (30 min)

### A. Cambios de paleta — "Llamas Cósmicas"

| Elemento                         | Original                                  | Versión personalizada                 |
| -------------------------------- | ----------------------------------------- | ------------------------------------- |
| `tailwind.config` → `surface`    | `#170d2c` (morado oscuro)                 | `#0c0200` (rojo-negro cósmico)        |
| `tailwind.config` → `primary`    | `#deb7ff` (lila)                          | `#fb923c` (naranja fuego)             |
| `tailwind.config` → `on-surface` | `#eaddff` (blanco lila)                   | `#fde8d8` (blanco anaranjado)         |
| `setup()` color inicial          | `color(222, 183, 255)`                    | `color(251, 146, 60)`                 |
| Botones de color                 | Primario/Rojo/Teal/Amarillo/Verde/Naranja | Fuego/Coral/Ámbar/Rosa/Magenta/Dorado |

Fuente de referencia de paleta: [colorhunt.co](https://colorhunt.co) (paletas cálidas de fuego)

---

### B. Cambios de comportamiento de partículas

```javascript
// ANTES (código base):
this.velocidadBrillo = random(0.018, 0.07); // Parpadeo lento
circle(this.x, this.y, this.tamano * 5); // Halo ×5

this.tamano = random(0.4, 2.2); // estrellas normales
this.tamano = random(1.5, 4); // estrellas de colisión

// DESPUÉS (mi versión personalizada):
this.velocidadBrillo = random(0.03, 0.1); // Parpadeo +43% más rápido
circle(this.x, this.y, this.tamano * 6); // Halo más visible ×6

this.tamano = random(0.4, 2.5); // normales: ligeramente más grandes
this.tamano = random(1.5, 4.5); // colisión: ligeramente más grandes

// Amplitud de parpadeo: sin() * 55 → sin() * 60 (más variación)
// Burst por clic: 5 → 8 partículas por defecto
// Slider máximo: 20 → 25 partículas
```

---

### C. Modo `'supernova'` — Creado en Fase 2

```javascript
} else if (modo === 'supernova') {
    // 50 partículas muy rápidas lanzadas desde el centro de la pantalla
    for (let i = 0; i < 50; i++) {
        let e = new Estrella(width / 2, height / 2, 'colision');
        e.vx    = random(-9, 9);  // velocidad ×2 respecto a colisión normal
        e.vy    = random(-9, 9);
        e.tamano = random(2, 7);
        e.vida  = 400;            // viven más para cubrir más distancia
        estrellas.push(e);
    }
}
```

**¿Por qué es diferente a los otros modos?**

- _Nebulosa_: estrellas estáticas, dispersas, permanentes (tipo `'normal'`)
- _Constelación_: pocas estrellas grandes, fijas, sin movimiento
- _Supernova_: muchas partículas muy rápidas desde el centro, efímeras (se auto-eliminan)

### D. Modo `'apagar'` y `'limpiar'`

```javascript
// 'apagar' — alterna pausa / reanudación
if (!pausado) {
	noLoop();
	pausado = true;
} else {
	loop();
	pausado = false;
}

// 'limpiar' — conserva fondo, elimina dinámicas
estrellas = estrellas.filter((e) => e.tipo === 'normal');
```

---

## ✅ FASE 3: Depuración y Resiliencia (25 min)

_(Ver [errores-corregidos.txt](errores-corregidos.txt) para el detalle completo)_

### Resumen de errores corregidos

| #           | Tipo       | Síntoma                                        | Causa                                               | Solución                             |
| ----------- | ---------- | ---------------------------------------------- | --------------------------------------------------- | ------------------------------------ |
| 1 (Error A) | Lógico     | Navegador se congela                           | `i++` en lugar de `i--` en el bucle → loop infinito | Cambiar `i++` → `i--`                |
| 2 (Error B) | Referencia | Canvas aparece al final del body sin ser fondo | `canvas.parent('canvas-contenedor')` → ID no existe | Usar `canvas.parent('p5-container')` |

### ¿Cómo los encontré?

**Error 1:**

1. _Observé_ que el navegador se congeló al lanzar partículas
2. Cerré la pestaña y abrí de nuevo
3. Identifiqué que el último cambio fue en el bucle `for` de eliminación
4. Comparé `i++` con la lógica esperada: debería decrementar, no incrementar
5. _Tipo de error_: **Lógico** (el código es sintácticamente válido pero produce comportamiento incorrecto)

**Error 2:**

1. _Observé_ que el canvas aparecía abajo del body en lugar de ser el fondo
2. Abrí F12 → Console: sin error rojo pero se veía el canvas como `<canvas>` solo en el DOM
3. Comparé el ID en `canvas.parent()` con el ID del div en el HTML
4. Encontré `'canvas-contenedor'` vs `'p5-container'` — no coinciden
5. _Tipo de error_: **Referencia** (ID que no existe en el DOM)

---

## ✅ FASE 4: Documentación y Entrega (15 min)

### Secciones documentadas en el código

| Sección                    | Tipo                                            | Descripción en comentarios                         |
| -------------------------- | ----------------------------------------------- | -------------------------------------------------- |
| Variables globales + setup | `// ==========================================` | Autor, fecha, propósito, personalización           |
| Clase `Estrella`           | `// ==========================================` | Propósito + 4 métodos documentados individualmente |
| `cambiarModo()`            | Comentario inline                               | Cada modo explicado con su comportamiento          |
| `changeColor()`            | Comentario inline                               | Documenta comunicación DOM ↔ p5.js                 |
| `updateStats()`            | Comentario inline                               | Explica optimización de 10 frames                  |
| Final del HTML             | `<!-- ==================== -->`                 | Guía de usuario completa                           |

### Checklist de entrega

- [x] `index.html` funciona al abrir en navegador
- [x] Consola (F12) sin errores rojos
- [x] Botones Nebulosa, Constelación, Supernova, Pausar y Limpiar funcionan
- [x] Clic en canvas crea explosión de partículas
- [x] Colores son distintos a los originales (paleta Llamas Cósmicas)
- [x] Comentarios de sección presentes (`// ====...`)
- [x] Clase `Estrella` documenta sus 4 métodos
- [x] Guía de usuario al final del HTML (`<!-- ====... -->`)
- [x] Nombre del autor en documentación, comentario de sección y guía
- [x] `errores-corregidos.txt` incluido con 2 errores documentados

### Estructura de entrega

```
my-first-interactive-galaxy/
├── index.html                               ← Galaxia personalizada + documentación
├── mi-galaxia-base.html                     ← Archivo base proporcionado por el docente
├── errores-corregidos.txt                   ← Fase 3: 2 errores diagnosticados
├── p5js_tailwind.md                         ← Guía de clase (5 bloques, HTML interactivo)
├── Actividad_Mi_Primera_Galaxia_Interactiva.md  ← Enunciado de la actividad
├── Desarrollo_Mi_Primera_Galaxia_Interactiva.md ← Este archivo (registro de trabajo)
└── README.md                                ← Descripción general del proyecto
```

---

## Reflexión Final

La experiencia más valiosa fue la **Fase 3 (depuración)**. El Error A (bucle infinito con `i++`) fue particularmente instructivo porque el síntoma —navegador congelado— no da ninguna pista textual. Solo al entender que un bucle `for` con condición `i >= 0` e incremento `i++` nunca termina, se puede diagnosticar correctamente.

La diferencia entre `setup()` y `draw()` es fundamental: confundirlos haría que el canvas se recree 60 veces por segundo (en `setup`) o que las estrellas iniciales solo aparezcan una vez (si se crean en `draw`).

El patrón de **comunicación DOM ↔ p5.js** (funciones globales llamadas desde `onclick`) es sencillo pero poderoso: permite que la interfaz HTML controle la lógica del canvas sin frameworks adicionales.
