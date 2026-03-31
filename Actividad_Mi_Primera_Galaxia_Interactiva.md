# Actividad: Mi Primera Galaxia Interactiva

**Diseño Web Interactivo • Nivel Básico**

- **Duración:** 90 minutos (1.5 horas)
- **Prerrequisito:** Código base proporcionado
- **Entrega:** Archivo `index.html` + documentación

---

## 🎯 Objetivo General

Comprender y personalizar una experiencia visual interactiva que combine diseño web moderno (Tailwind) con gráficos generativos (p5.js), demostrando capacidad de lectura de código, modificación controlada y resolución de problemas.

### 1. Objetivos Específicos

| # | Objetivo | Evidencia de Logro |
|---|----------|--------------------|
| 1 | Interpretar la estructura de un proyecto integrado Tailwind + p5.js | Explicar con sus palabras qué hace cada sección del código base proporcionado |
| 2 | Modificar parámetros visuales para personalizar la experiencia | Galaxia con paleta de colores y comportamientos distintivos al original |
| 3 | Depurar errores básicos usando la consola del navegador | Identificar y corregir 2+ problemas sin ayuda directa del docente |
| 4 | Documentar el funcionamiento del código para otros desarrolladores | Comentarios claros y sección de documentación al final del archivo |

---

### 2. Materiales Necesarios

| Para el Estudiante | Proporcionados por el Docente |
|--------------------|-------------------------------|
| Computadora con navegador Chrome/Firefox | Archivo `mi-galaxia-base.html` (código funcional) |
| Editor de código (VS Code recomendado) | Rúbrica de evaluación |
| Conexión a internet (para CDNs) | Checklist de verificación por fases |
| Esta guía de actividad | |

---

## Fase 1: Exploración y Comprensión ⏱️ 20 minutos

**Objetivo:** Entender qué hace cada parte del código antes de modificarlo.

### A. Ejecutar y observar

1. Abre el archivo `mi-galaxia-base.html` en tu navegador
2. Interactúa con todos los botones: Nebulosa, Constelación, Apagar, Limpiar
3. Haz click en diferentes partes del canvas (área de la galaxia)
4. Cambia los colores usando los botones circulares inferiores

### B. Mapeo mental

En tu cuaderno o archivo de texto, responde estas preguntas de comprensión:

**Sección HTML (Tailwind):**
- ☐ ¿Qué hace la clase `"fixed inset-0 -z-10"`?
- ☐ ¿Para qué sirve el atributo `onclick="cambiarModo('nebulosa')"`?
- ☐ ¿Qué significa `"backdrop-blur-xl"` visualmente?

**Sección JavaScript (p5.js):**
- ☐ ¿Cuándo se ejecuta `setup()` vs `draw()`?
- ☐ ¿Qué representa la clase `Estrella`?
- ☐ ¿Qué diferencia hay entre una estrella de tipo `'normal'` y `'colision'`?

### C. Predicción (antes de probar)

Antes de modificar el código, predice qué pasará si:

- Cambias el número `80` en `cambiarModo('nebulosa')` a `200`
- Cambias `this.vida -= 3` a `this.vida -= 10`
- Cambias `random(-4, 4)` a `random(-10, 10)`

### ✅ Verificación de Fase 1

- [ ] He interactuado con todos los controles
- [ ] Tengo respuestas escritas para las 6 preguntas
- [ ] He hecho 3 predicciones antes de probar

---

## Fase 2: Personalización Visual ⏱️ 30 minutos

**Objetivo:** Modificar parámetros para crear una galaxia única con identidad propia.

### A. Modificar paleta de colores

Ubica estas líneas en el código y cámbialas:

| Ubicación | Original | Tu Versión | Efecto |
|-----------|----------|------------|--------|
| `tailwind.config` | `primary: '#deb7ff'` | Tu color HEX | Color principal UI |
| `tailwind.config` | `accent: '#00d9ff'` | Otro color HEX | Color de acento |
| `setup()` | `color(222, 183, 255)` | `color(R, G, B)` | Color inicial estrellas |

> 💡 Herramientas recomendadas: [colorhunt.co](https://colorhunt.co) o [coolors.co](https://coolors.co) para elegir paletas harmoniosas.

### B. Modificar comportamiento de partículas

En la clase `Estrella`, ajusta estos valores:

```javascript
// En el constructor, según el tipo:
if (tipo === 'colision') {
    this.vx = random(-4, 4); // ← Cambiar rango velocidad
    this.vy = random(-4, 4);
    this.vida = 255; // ← Cambiar a 500 para durar más
    // ...
} else {
    this.vx = random(-0.5, 0.5); // ← Cambiar para movimiento rápido/lento
    this.vy = random(-0.5, 0.5);
    // ...
}

// En actualizar():
this.velocidadBrillo = random(0.02, 0.06); // ← 0.1 = parpadeo rápido

// En mostrar():
circle(this.x, this.y, this.tamano * 4); // ← Cambiar 4 para más/menos glow
```

### C. Modificar modos de visualización

En la función `cambiarModo()`, experimenta:

```javascript
if (modo === 'nebulosa') {
    for (let i = 0; i < 80; i++) { // ← Cambiar cantidad
        estrellas.push(new Estrella());
    }
} else if (modo === 'constelacion') {
    for (let i = 0; i < 15; i++) {
        let e = new Estrella();
        e.tamano = random(4, 10); // ← Cambiar rango tamaño
        // NUEVO: Agregar comportamiento especial
        e.vx = 0; // Estrellas fijas
        e.vy = 0;
        estrellas.push(e);
    }
}
```

### D. Crear tu propio modo: `'supernova'`

**Paso 1:** Agrega botón en HTML:

```html
<button onclick="cambiarModo('supernova')" 
    class="py-3 px-4 rounded-xl bg-orange-500/20 
    border border-orange-500/30 text-orange-300">
    💥 Supernova
</button>
```

**Paso 2:** Agrega lógica en JavaScript:

```javascript
else if (modo === 'supernova') {
    // Tu lógica: muchas estrellas, muy rápidas, duración corta
    for (let i = 0; i < ___; i++) {
        let e = new Estrella();
        // Modifica propiedades antes de agregar:
        e.vx = random(___, ___);
        e.vy = random(___, ___);
        e.tamano = random(___, ___);
        estrellas.push(e);
    }
}
```

### ✅ Verificación de Fase 2

- [ ] Tengo colores personalizados (no los originales púrpura/cyan)
- [ ] Las estrellas se comportan diferente (velocidad/brillo/tamaño)
- [ ] Mi modo `'supernova'` funciona y es distinto a los otros
- [ ] He guardado versiones intermedias (Ctrl+S frecuentemente)

---

## Fase 3: Depuración y Resiliencia ⏱️ 25 minutos

**Objetivo:** Aprender a identificar y corregir errores sin pánico.

### A. Introducir errores controlados

El docente te asignará 2 errores de esta lista (o elige 2 si trabajas autónomamente):

| Error | Descripción | Síntoma Esperado |
|-------|-------------|------------------|
| A: Sintaxis | Cambiar `i--` por `i++` en el bucle de eliminación | Navegador se congela o estrellas no desaparecen |
| B: Referencia | Cambiar ID `'canvas-container'` por `'canvas-contenedor'` | Canvas aparece al final de página o no aparece |
| C: Lógica | Cambiar `this.vida -= 3` por `this.vida += 3` | Estrellas de colisión nunca desaparecen |

### B. Protocolo de diagnóstico

Para cada error, sigue estos pasos:

1. **Observa:** ¿Qué síntoma aparece? (pantalla blanca, congelamiento, comportamiento extraño)
2. **Abre consola:** Presiona `F12` → pestaña Console
3. **Lee el error:** ¿Qué línea menciona? ¿Qué tipo de error es (`SyntaxError`, `ReferenceError`, `TypeError`)?
4. **Corrige:** Vuelve al código y arregla basándote en el mensaje
5. **Verifica:** Refresca (`F5`) y confirma que funciona

### C. Documentación del error

Crea archivo `errores-corregidos.txt` con este formato:

```
ERROR #1
--------
Síntoma: [Lo que veías en pantalla]
Mensaje en consola: [Copiar texto exacto]
Línea afectada: [Número de línea aproximado]
Causa real: [Tu explicación en palabras propias]
Solución: [Qué cambiaste para arreglarlo]

ERROR #2
--------
[Idem]
```

### ✅ Verificación de Fase 3

- [ ] He corregido 2 errores sin pedir la solución directa
- [ ] Tengo documentado cada error con sus 5 campos
- [ ] Sé abrir la consola del navegador (F12)
- [ ] Puedo identificar si un error es de sintaxis, referencia o lógica

---

## Fase 4: Documentación y Entrega ⏱️ 15 minutos

**Objetivo:** Dejar el código listo para que otros lo entiendan y usen.

### A. Comentar el código

Asegúrate de tener comentarios en estas secciones mínimas:

```javascript
// ==========================================
// SECCIÓN 1: CONFIGURACIÓN INICIAL
// Autor: [Tu nombre completo]
// Propósito: Establecer el entorno visual básico
// ==========================================

// ==========================================
// SECCIÓN 2: CLASE ESTRELLA
// Propósito: Definir el comportamiento de cada partícula
// Métodos:
// - constructor(): Crea la estrella con propiedades iniciales
// - actualizar(): Modifica posición y estado cada frame
// - mostrar(): Dibuja la estrella en pantalla
// - estaMuerta(): Verifica si debe eliminarse
// ==========================================
```

### B. Crear guía de usuario

Al final del HTML, antes de `</body>`, agrega:

```html
<!-- 
==========================================
GUÍA DE USUARIO - MI GALAXIA v1.0
Por: [Tu nombre completo]
Fecha: [Fecha de entrega]

CÓMO USAR:
1. Hacer click en "Nebulosa" para [describir qué hace]
2. Hacer click en "Constelación" para [describir qué hace]
3. Hacer click en "Supernova" para [describir tu modo]
4. Click en canvas: crea explosión de estrellas
5. Botones de color: cambian toda la paleta

PERSONALIZACIONES REALIZADAS:
- Colores: [describir tu paleta elegida]
- Velocidad: [más lenta/más rápida/igual que original]
- Efectos especiales: [qué agregaste de nuevo]

CRÉDITOS:
Basado en guía de clase "Cosmos Interactivo"
Tecnologías: HTML5, Tailwind CSS, p5.js
==========================================
-->
```

### C. Preparar estructura de entrega

Tu carpeta debe contener estos archivos:

```
mi-galaxia/
├── index.html (archivo principal funcional)
├── errores-corregidos.txt (documentación Fase 3)
└── README.txt (opcional: instrucciones de instalación)
```

### ✅ Verificación de Fase 4

- [ ] Cada función tiene comentario de propósito
- [ ] La clase `Estrella` documenta sus 4 métodos
- [ ] Tengo guía de usuario para alguien que nunca vio el código
- [ ] Mi nombre aparece en 3 lugares: título, comentarios, guía

---

## 3. Rúbrica de Evaluación (100 puntos)

| Criterio | Pts. | Excelente (100%) | Satisfactorio (70%) | En desarrollo (40%) | Insuficiente (0%) |
|----------|------|------------------|---------------------|---------------------|-------------------|
| Comprensión del código | 20 | Explica cada sección con precisión técnica, identifica flujo de datos | Explica la mayoría de secciones, algunas imprecisiones menores | Explica solo secciones superficiales, confunde conceptos clave | No puede explicar qué hace el código |
| Personalización visual | 25 | Paleta coherente, 3+ modificaciones de comportamiento, modo 'supernova' funcional y distintivo | Paleta modificada, 2 modificaciones, modo nuevo básico | Solo colores cambiados, o modificaciones que no funcionan | Sin cambios respecto al código base |
| Depuración | 25 | Corrige 2+ errores independientemente, documenta con precisión causa y solución | Corrige 2 errores con mínima ayuda, documentación adecuada | Corrige 1 error o requiere ayuda sustancial para ambos | No puede corregir errores ni identificarlos |
| Documentación | 20 | Comentarios explican "por qué" no solo "qué", guía de usuario clara para terceros | Comentarios en todas secciones, guía de usuario básica | Comentarios incompletos o solo en algunas secciones | Sin comentarios o sin guía de usuario |
| Entrega técnica | 10 | Archivo funciona al abrir, sin errores en consola, estructura de carpetas correcta | Funciona con advertencias menores, estructura aceptable | Funciona con errores no críticos, desorganizado | No funciona o faltan archivos |

**Escala de Calificación:** 90-100 Excelente • 80-89 Muy Bueno • 70-79 Bueno • 60-69 Suficiente • <60 Insuficiente

---

## Formato de Entrega

| Campo | Detalle |
|-------|---------|
| Nombre del estudiante | |
| Fecha de entrega | |
| Nombre del archivo principal | `index.html` |
| Archivos adjuntos | `errores-corregidos.txt` |
| URL de repositorio (opcional) | |
| Observaciones del docente | |
| Calificación numérica | / 100 |
| Calificación cualitativa | |

---

## 🎁 Extensiones Opcionales (Para quienes terminan antes)

| Nivel | Tiempo | Desafío |
|-------|--------|---------|
| 1: Fácil | 10 min | Agregar quinto color a la paleta • Cambiar forma del cursor (círculo → cuadrado) • Modificar texto del título principal |
| 2: Medio | 20 min | Agregar sonido al hacer click (p5.sound) • Efecto de gravedad en modo supernova • Fondo que cambia de color gradualmente |
| 3: Desafío | 30+ min | Slider HTML que controle velocidad global • "Modo hipersalto" con líneas rectas largas • Sistema de "constelaciones guardadas" con posiciones fijas |

---

## 4. Checklist Final de Entrega

Antes de enviar, verifica cada ítem:

- [ ] Archivo se llama `index.html`
- [ ] Abre correctamente en navegador
- [ ] Consola (F12) sin errores rojos
- [ ] Todos los botones funcionan
- [ ] Click en canvas crea explosión
- [ ] Colores son diferentes a originales
- [ ] Comentarios explicativos presentes
- [ ] Guía de usuario al final del HTML
- [ ] Tu nombre aparece en documentación
- [ ] Archivo `errores-corregidos.txt` incluido

---

## 5. Protocolo de Ayuda Permitida

| Si te atoras en... | Pregunta permitida ✅ | No se permite ❌ |
|--------------------|----------------------|-----------------|
| Fase 1 (Comprensión) | "¿Esta parte del código controla la apariencia o el comportamiento?" | "¿Qué hace esta función exactamente?" (debes inferir) |
| Fase 2 (Personalización) | "¿En qué línea aproximada puedo cambiar la velocidad?" | "Dame los números exactos para que se vea bien" |
| Fase 3 (Depuración) | "¿Este error es de sintaxis, referencia o lógica?" | "Arréglalo por mí" |

---

*Diseño Web Interactivo • Actividad práctica con p5.js y Tailwind CSS*