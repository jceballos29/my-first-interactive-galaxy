# Guía de Clase: p5.js + Tailwind CSS

**Diseño Web Interactivo • Programación Creativa**

- **Duración total:** ~2 horas (6 bloques de 15–25 min)
- **Meta:** Construir paso a paso una experiencia visual desde un canvas vacío hasta un sistema de partículas con controles de color
- **Tecnologías:** p5.js 1.9.x · Tailwind CSS CDN · HTML + JavaScript vanilla

> **Cómo seguir esta guía:** Cada bloque entrega código funcional que se acumula sobre el anterior. Completa la verificación al final de cada bloque antes de continuar.

---

## Progreso

| Bloque | Tema                                  | Tiempo   | Estado |
| ------ | ------------------------------------- | -------- | ------ |
| 0      | Estructura Base HTML + Tailwind       | 15 min   | ☐      |
| 1      | Integrar p5.js — Canvas Básico        | 20 min   | ☐      |
| 2      | Sistema de Partículas (OOP)           | 25 min   | ☐      |
| 3      | Interacción con Mouse                 | 20 min   | ☐      |
| 4      | Comunicación Bidireccional            | 20 min   | ☐      |
| 5      | Stats en Tiempo Real + Optimizaciones | 20 min   | ☐      |
| —      | Cheatsheet de Referencia              | consulta | —      |

---

## Bloque 0: Estructura Base HTML + Tailwind ⏱️ 15 min

**Configuración del entorno visual**

### 🎯 Objetivos

- [ ] Configurar tema oscuro personalizado en Tailwind
- [ ] Crear layout responsive con glassmorphism
- [ ] Preparar el contenedor `#p5-container` para el canvas de p5.js

### ⚠️ Importante

Crea un archivo nuevo llamado `index.html` y copia el código completo a continuación.

### 📝 Pasos

1. Configura Tailwind con el tema de colores **"Cosmos"**
2. Crea el contenedor `#p5-container` con clases `fixed inset-0 -z-10`
3. Construye la UI: header, card de controles y stats

### Código — `bloque-0-base.html`

```html
<!DOCTYPE html>
<html class="dark" lang="es">
	<head>
		<meta charset="utf-8" />
		<meta
			name="viewport"
			content="width=device-width, initial-scale=1.0"
		/>
		<title>Cosmos - Base</title>

		<!-- 1. CDN de Tailwind -->
		<script src="https://cdn.tailwindcss.com"></script>

		<!-- 2. Configuración del tema -->
		<script>
			tailwind.config = {
				darkMode: 'class',
				theme: {
					extend: {
						colors: {
							surface: '#170d2c',
							primary: '#deb7ff',
							'on-surface': '#eaddff',
							'surface-variant': '#3a2f50',
						},
					},
				},
			};
		</script>

		<style>
			body {
				font-family: 'Inter', sans-serif;
			}
		</style>
	</head>

	<!-- 3. Body con tema oscuro -->
	<body
		class="bg-surface text-on-surface min-h-screen overflow-x-hidden"
	>
		<!-- 4. CONTENEDOR PARA P5.JS (vacío por ahora) -->
		<div
			id="p5-container"
			class="fixed inset-0 -z-10 bg-surface-variant"
		>
			<!-- Placeholder visual — estrellas estáticas decorativas -->
			<div class="absolute inset-0 opacity-30">
				<div
					class="absolute top-1/4 left-1/4 w-2 h-2 bg-primary rounded-full"
				></div>
				<div
					class="absolute top-1/3 right-1/3 w-1 h-1 bg-primary rounded-full"
				></div>
			</div>
		</div>

		<!-- 5. CONTENIDO PRINCIPAL -->
		<main
			class="relative z-10 container mx-auto px-6 py-12 
                 min-h-screen flex flex-col items-center justify-center"
		>
			<div class="max-w-2xl w-full space-y-8">
				<!-- HEADER -->
				<div class="text-center space-y-4">
					<h1
						class="text-5xl md:text-7xl font-bold text-primary 
                           tracking-tight drop-shadow-[0_0_30px_rgba(222,183,255,0.5)]"
					>
						Cosmos
					</h1>
					<p class="text-lg text-on-surface/80 max-w-md mx-auto">
						Tu primer canvas p5.js integrado con Tailwind CSS
					</p>
				</div>

				<!-- CARD DE CONTROLES (deshabilitada por ahora) -->
				<div
					class="bg-surface-variant/60 backdrop-blur-xl rounded-2xl p-8 
                        border border-primary/20 shadow-[0_0_40px_rgba(123,44,191,0.2)]"
				>
					<div class="flex items-center justify-between mb-6">
						<h2 class="text-2xl font-semibold text-primary">
							Controles
						</h2>
						<span
							class="px-3 py-1 bg-primary/20 text-primary text-xs rounded-full"
						>
							Próximamente
						</span>
					</div>

					<!-- Grid de botones (deshabilitados) -->
					<div class="grid grid-cols-2 gap-4 opacity-50">
						<button
							class="p-4 rounded-xl bg-red-500/20 border border-red-500/30"
						>
							<span class="font-semibold text-red-300">Rojo</span>
						</button>
						<button
							class="p-4 rounded-xl bg-teal-500/20 border border-teal-500/30"
						>
							<span class="font-semibold text-teal-300">Teal</span>
						</button>
						<button
							class="p-4 rounded-xl bg-yellow-500/20 border border-yellow-500/30"
						>
							<span class="font-semibold text-yellow-300"
								>Amarillo</span
							>
						</button>
						<button
							class="p-4 rounded-xl bg-purple-500/20 border border-purple-500/30"
						>
							<span class="font-semibold text-purple-300"
								>Primario</span
							>
						</button>
					</div>
				</div>

				<!-- STATS (estáticos) -->
				<div class="grid grid-cols-3 gap-4 text-center">
					<div class="bg-surface-variant/40 rounded-lg p-4">
						<p class="text-3xl font-bold text-primary">0</p>
						<p
							class="text-xs text-on-surface/60 uppercase tracking-wider"
						>
							Estrellas
						</p>
					</div>
					<div class="bg-surface-variant/40 rounded-lg p-4">
						<p class="text-3xl font-bold text-primary">--</p>
						<p
							class="text-xs text-on-surface/60 uppercase tracking-wider"
						>
							FPS
						</p>
					</div>
					<div class="bg-surface-variant/40 rounded-lg p-4">
						<p class="text-3xl font-bold text-primary">0,0</p>
						<p
							class="text-xs text-on-surface/60 uppercase tracking-wider"
						>
							Posición
						</p>
					</div>
				</div>
			</div>
		</main>
	</body>
</html>
```

### ✅ Verificación del Bloque 0

Abre el archivo en el navegador. Debes ver:

- [ ] Fondo morado oscuro (`#170d2c`)
- [ ] Título "Cosmos" con glow morado
- [ ] Card con glassmorphism (efecto translúcido)
- [ ] 4 botones deshabilitados en grid 2×2
- [ ] 3 stats en la parte inferior (Estrellas / FPS / Posición)

---

## Bloque 1: Integrar p5.js — Canvas Básico ⏱️ 20 min

**Primer canvas interactivo**

### 🎯 Objetivos

- [ ] Agregar p5.js vía CDN
- [ ] Crear canvas que ocupe toda la ventana
- [ ] Conectar p5.js con el contenedor HTML (`canvas.parent()`)
- [ ] Dibujar un círculo que siga el mouse

### 📚 Conceptos Clave

| Función               | Descripción                                          |
| --------------------- | ---------------------------------------------------- |
| `createCanvas(w, h)`  | Crea el canvas con dimensiones dadas                 |
| `canvas.parent('id')` | Mueve el canvas dentro de un elemento HTML           |
| `draw()`              | Se ejecuta ~60 veces por segundo                     |
| `windowResized()`     | Se llama automáticamente al redimensionar la ventana |

### 📝 Pasos

1. Agrega el CDN de p5.js **antes de `</body>`**
2. Crea las funciones `setup()` y `draw()`
3. Usa `canvas.parent('p5-container')` para anclar el canvas al div
4. Dibuja `circle(mouseX, mouseY, 50)` para verificar interactividad

### Código — `Modificaciones al <body>`

```javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.4/p5.min.js"></script>
<script>
    // ==========================================
    // BLOQUE 1: Canvas Básico
    // ==========================================
    let stars = [];

    function setup() {
        let canvas = createCanvas(windowWidth, windowHeight);
        canvas.parent('p5-container');
        console.log('✅ p5.js inicializado');
        console.log('Tamaño:', width, 'x', height);
    }

    function draw() {
        background(23, 13, 44);          // Fondo morado sólido
        fill(222, 183, 255);             // Color morado claro
        noStroke();
        circle(mouseX, mouseY, 50);     // Círculo sigue el mouse
    }

    function windowResized() {
        resizeCanvas(windowWidth, windowHeight);
    }
</script>
```

### ✅ Verificación del Bloque 1

- [ ] El canvas reemplaza el fondo estático morado
- [ ] Un círculo morado sigue el cursor del mouse
- [ ] La UI de Tailwind (título, card, stats) sigue visible encima del canvas
- [ ] Al redimensionar la ventana, el canvas se adapta
- [ ] En la consola del navegador aparece "✅ p5.js inicializado"

---

## Bloque 2: Sistema de Partículas ⏱️ 25 min

**Programación Orientada a Objetos**

### 🎯 Objetivos

- [ ] Crear la clase `Star` con constructor, `update()` y `display()`
- [ ] Generar 100 instancias al inicio
- [ ] Iterar el array con `for...of`
- [ ] Agregar efecto de estela con `background(r, g, b, alpha)`

### 📐 Patrón de Diseño

> Esta implementación aplica el patrón **Object Pool**: crear todos los objetos de antemano en lugar de crearlos y destruirlos constantemente, reduciendo el costo de garbage collection.

### Anatomía de una Clase

```javascript
class NombreClase {
	constructor() {
		this.propiedad = valor; // Estado del objeto
	}

	metodo() {
		// Comportamiento usando this.propiedad
	}
}

// Crear instancia
let objeto = new NombreClase();
```

### 📝 Pasos

1. Definir la clase `Star` con todas las propiedades en el constructor
2. Crear 100 instancias en `setup()` con un loop `for`
3. Iterar con `for (let star of stars)` en `draw()`
4. Usar `background(23, 13, 44, 30)` para crear efecto de estela

### Código — `Script completo Bloque 2`

```javascript
<script>
    // ==========================================
    // BLOQUE 2: Sistema de Partículas
    // ==========================================
    let stars = [];
    let starColor;

    function setup() {
        let canvas = createCanvas(windowWidth, windowHeight);
        canvas.parent('p5-container');

        starColor = color(222, 183, 255);  // Morado claro

        // Crear 100 estrellas iniciales
        for (let i = 0; i < 100; i++) {
            stars.push(new Star());
        }
    }

    function draw() {
        background(23, 13, 44, 30);   // Alpha bajo = efecto de estela

        // Actualizar y dibujar cada estrella
        for (let star of stars) {
            star.update();
            star.display();
        }

        // Cursor personalizado: núcleo + anillo
        noCursor();
        fill(starColor);
        noStroke();
        circle(mouseX, mouseY, 20);   // Núcleo sólido
        noFill();
        stroke(starColor);
        strokeWeight(2);
        circle(mouseX, mouseY, 40);   // Anillo exterior
    }

    function windowResized() {
        resizeCanvas(windowWidth, windowHeight);
    }

    // ==========================================
    // CLASE STAR
    // ==========================================
    class Star {
        constructor() {
            // Posición aleatoria en toda la pantalla
            this.x = random(width);
            this.y = random(height);

            // Tamaño: pequeñas puntitas de luz
            this.size = random(0.5, 3);

            // Parpadeo: ángulo inicial aleatorio para que no sincronicen
            this.baseAlpha = random(100, 255);
            this.alpha = this.baseAlpha;
            this.twinkleSpeed = random(0.02, 0.08);
            this.twinkleOffset = random(TWO_PI);

            // Color (se puede cambiar después)
            this.col = starColor;
        }

        update() {
            // Fórmula de parpadeo: alpha = base + sin(ángulo) × amplitud
            // Ejemplo: 200 + sin(3.14) × 50 = 150
            this.twinkleOffset += this.twinkleSpeed;
            this.alpha = this.baseAlpha + sin(this.twinkleOffset) * 50;
            this.alpha = constrain(this.alpha, 50, 255);
        }

        display() {
            noStroke();
            fill(red(this.col), green(this.col), blue(this.col), this.alpha);
            circle(this.x, this.y, this.size);

            // Halo de resplandor para estrellas grandes
            if (this.size > 2) {
                fill(red(this.col), green(this.col), blue(this.col), this.alpha * 0.3);
                circle(this.x, this.y, this.size * 3);
            }
        }
    }
</script>
```

### ✅ Verificación del Bloque 2

- [ ] 100 estrellas distribuidas aleatoriamente en la pantalla
- [ ] Las estrellas parpadean de forma asíncrona (no al mismo ritmo)
- [ ] Las estrellas de tamaño > 2 tienen un halo difuso alrededor
- [ ] Al mover el mouse, se dibuja el cursor personalizado (núcleo + anillo)
- [ ] Al arrastrar el mouse rápido, se ve la estela de movimiento

---

## Bloque 3: Interacción con Mouse ⏱️ 20 min

**Eventos y estados dinámicos**

### 🎯 Objetivos

- [ ] Detectar clicks con `mousePressed()`
- [ ] Crear estrellas "nuevas" con velocidad y vida limitada
- [ ] Distinguir estrellas estáticas (permanentes) de dinámicas (temporales)
- [ ] Actualizar el contador en el DOM (HTML ↔ p5.js)

### ⚠️ Cambios en la Clase Star

El constructor ahora acepta parámetros opcionales. Las estrellas pueden ser:

| Tipo          | Creada en                           | Comportamiento                     |
| ------------- | ----------------------------------- | ---------------------------------- |
| **Estáticas** | `setup()` — sin parámetros          | Viven para siempre, solo parpadean |
| **Dinámicas** | `mousePressed()` — con `isNew=true` | Se mueven, se desvanecen y mueren  |

### 📝 Pasos

1. Modificar constructor: `new Star(x, y, isNew)`
2. Agregar propiedades: `vx`, `vy`, `life`, `isNew`
3. Crear función `mousePressed()`
4. Crear `updateStarCount()` para modificar el DOM

> **Nota para el siguiente bloque:** Las estrellas muertas aún no se eliminan del array. En el Bloque 4 agregaremos la iteración inversa con `splice()`.

### Código — `Modificaciones al script anterior`

```javascript
<script>
    // ==========================================
    // BLOQUE 3: Interacción con Mouse
    // ==========================================
    let stars = [];
    let starColor;
    let currentColor;  // Para el cursor

    function setup() {
        let canvas = createCanvas(windowWidth, windowHeight);
        canvas.parent('p5-container');

        starColor = color(222, 183, 255);
        currentColor = starColor;

        // Estrellas estáticas iniciales (sin parámetros = estática)
        for (let i = 0; i < 100; i++) {
            stars.push(new Star());
        }
    }

    function draw() {
        background(23, 13, 44, 30);

        for (let star of stars) {
            star.update();
            star.display();
        }

        // Cursor (sin cambios del bloque anterior)
        noCursor();
        noFill();
        stroke(currentColor);
        strokeWeight(2);
        circle(mouseX, mouseY, 40);
        fill(currentColor);
        noStroke();
        circle(mouseX, mouseY, 20);
    }

    // ==========================================
    // NUEVO: Evento de click
    // ==========================================
    function mousePressed() {
        console.log('🖱️ Click en:', mouseX, mouseY);

        // Crear 5 estrellas "nuevas" en la posición del mouse
        for (let i = 0; i < 5; i++) {
            stars.push(new Star(mouseX, mouseY, true));
        }

        updateStarCount();
    }

    // ==========================================
    // NUEVO: Comunicación con DOM
    // ==========================================
    function updateStarCount() {
        let countElement = document.getElementById('star-count');
        if (countElement) {
            countElement.textContent = stars.length;
        }
    }

    function windowResized() {
        resizeCanvas(windowWidth, windowHeight);
    }

    // ==========================================
    // CLASE STAR MODIFICADA
    // ==========================================
    class Star {
        // Constructor con parámetros opcionales
        constructor(x, y, isNew = false) {

            if (isNew) {
                // Estrella DINÁMICA (creada por click)
                this.x = x + random(-20, 20);   // Dispersión alrededor del mouse
                this.y = y + random(-20, 20);
                this.vx = random(-3, 3);         // Velocidad aleatoria
                this.vy = random(-3, 3);
                this.life = 255;                 // Vida que se agota
                this.isNew = true;

            } else {
                // Estrella ESTÁTICA (creada al inicio)
                this.x = random(width);
                this.y = random(height);
                this.vx = 0;
                this.vy = 0;
                this.life = -1;  // -1 = infinito
                this.isNew = false;
            }

            // Propiedades comunes
            this.size = random(0.5, 3);
            this.baseAlpha = random(100, 255);
            this.alpha = this.baseAlpha;
            this.twinkleSpeed = random(0.02, 0.08);
            this.twinkleOffset = random(TWO_PI);
            this.col = starColor;
        }

        update() {
            if (this.isNew) {
                this.x += this.vx;    // Mover
                this.y += this.vy;
                this.life -= 3;        // Reducir vida
                this.alpha = this.life; // Opacidad = vida restante

            } else {
                // Estática: solo parpadear
                this.twinkleOffset += this.twinkleSpeed;
                this.alpha = this.baseAlpha + sin(this.twinkleOffset) * 50;
                this.alpha = constrain(this.alpha, 50, 255);
            }
        }

        display() {
            if (this.alpha <= 0) return;  // No dibujar si está "muerta"

            noStroke();
            fill(red(this.col), green(this.col), blue(this.col), this.alpha);
            circle(this.x, this.y, this.size);

            if (this.size > 2 || this.isNew) {
                fill(red(this.col), green(this.col), blue(this.col), this.alpha * 0.3);
                circle(this.x, this.y, this.size * 3);
            }
        }

        // NUEVO: Método para saber si debe eliminarse
        isDead() {
            return this.isNew && this.life <= 0;
        }
    }
</script>
```

### ✅ Verificación del Bloque 3

- [ ] Al hacer click aparecen 5 estrellas nuevas (explosión pequeña)
- [ ] Las estrellas nuevas se mueven y se desvanecen gradualmente
- [ ] El contador "Estrellas" del HTML aumenta con cada click
- [ ] En la consola aparecen las coordenadas de cada click

---

## Bloque 4: Comunicación Bidireccional ⏱️ 20 min

**DOM ↔ p5.js**

### 🎯 Objetivos

- [ ] Habilitar botones HTML con `onclick`
- [ ] Crear función global `changeColor()`
- [ ] Eliminar estrellas muertas del array (optimización de memoria)

### ✨ Momento Clave

Este bloque conecta los dos mundos: el HTML estático de Tailwind con el canvas dinámico de p5.js. Los botones ahora controlan el código creativo.

### 📝 Dos archivos a modificar

**1. HTML — Reemplazar los botones deshabilitados:**

```html
<div class="grid grid-cols-2 gap-4">
	<button
		onclick="changeColor('#ff6b6b')"
		class="p-4 rounded-xl bg-red-500/20 border border-red-500/30 
                   hover:scale-105 transition-transform cursor-pointer"
	>
		<span class="font-semibold text-red-300">Rojo</span>
	</button>

	<button
		onclick="changeColor('#4ecdc4')"
		class="p-4 rounded-xl bg-teal-500/20 border border-teal-500/30 
                   hover:scale-105 transition-transform cursor-pointer"
	>
		<span class="font-semibold text-teal-300">Teal</span>
	</button>

	<button
		onclick="changeColor('#ffe66d')"
		class="p-4 rounded-xl bg-yellow-500/20 border border-yellow-500/30 
                   hover:scale-105 transition-transform cursor-pointer"
	>
		<span class="font-semibold text-yellow-300">Amarillo</span>
	</button>

	<button
		onclick="changeColor('#deb7ff')"
		class="p-4 rounded-xl bg-purple-500/20 border border-purple-500/30 
                   hover:scale-105 transition-transform cursor-pointer"
	>
		<span class="font-semibold text-purple-300">Primario</span>
	</button>
</div>
```

**2. JavaScript — Agregar al final del script:**

```javascript
// ==========================================
// NUEVA FUNCIÓN: Cambiar color desde HTML
// ==========================================
function changeColor(hexColor) {
	console.log('🎨 Cambiando color a:', hexColor);

	// Convertir string hex a color p5.js
	let newColor = color(hexColor);

	// Actualizar variables globales
	currentColor = newColor;
	starColor = newColor;

	// Actualizar TODAS las estrellas existentes
	for (let star of stars) {
		star.col = newColor;
	}
}
```

### Código — `draw() modificado — Eliminación de estrellas muertas`

```javascript
function draw() {
	background(23, 13, 44, 30);

	// ==========================================
	// CAMBIO IMPORTANTE: Iterar al revés
	// ==========================================
	// Por qué al revés? Si eliminamos índice 5 mientras vamos hacia adelante,
	// el índice 6 se convierte en 5 y lo saltamos.
	// Yendo al revés, esto no importa.

	for (let i = stars.length - 1; i >= 0; i--) {
		stars[i].update();
		stars[i].display();

		if (stars[i].isDead()) {
			stars.splice(i, 1); // Eliminar del array
		}
	}

	// Actualizar contador cada 5 frames (no saturar el DOM)
	if (frameCount % 5 === 0) {
		updateStarCount();
	}

	// Cursor
	noCursor();
	noFill();
	stroke(currentColor);
	strokeWeight(2);
	circle(mouseX, mouseY, 40);
	fill(currentColor);
	noStroke();
	circle(mouseX, mouseY, 20);
}
```

### Comparativa: Iteración normal vs. inversa

|                          | Iteración normal `i++`                        | Iteración inversa `i--`                 |
| ------------------------ | --------------------------------------------- | --------------------------------------- |
| **Al eliminar índice 5** | El elemento en índice 6 "sube" a 5 y se salta | Los índices menores no se ven afectados |
| **Resultado**            | ❌ Se pierden elementos                       | ✅ Se elimina correctamente             |

```javascript
// ❌ PROBLEMA: iteración normal
for (let i = 0; i < array.length; i++) {
	if (array[i].isDead()) {
		array.splice(i, 1); // ¡El siguiente elemento se salta!
	}
}

// ✅ CORRECTO: iteración inversa
for (let i = array.length - 1; i >= 0; i--) {
	if (array[i].isDead()) {
		array.splice(i, 1); // No afecta índices menores
	}
}
```

### ✅ Verificación del Bloque 4

- [ ] Los 4 botones responden al hover (escalan ligeramente)
- [ ] Al hacer click en un botón, el cursor cambia de color
- [ ] Las estrellas nuevas usan el color seleccionado
- [ ] Las estrellas viejas también cambian al nuevo color
- [ ] El contador baja automáticamente cuando mueren estrellas
- [ ] No hay fugas de memoria (estrellas se eliminan correctamente)

---

## Bloque 5: Stats en Tiempo Real + Optimizaciones ⏱️ 20 min

**Performance y pulido**

### 🎯 Objetivos

- [ ] Mostrar FPS (frames por segundo) en tiempo real
- [ ] Mostrar posición del mouse en tiempo real
- [ ] Optimizar: no actualizar el DOM cada frame

### ⚡ ¿Por qué optimizar?

`draw()` se ejecuta 60 veces por segundo. Modificar el DOM (`element.textContent`) es una operación lenta. Si actualizamos stats cada frame, los FPS caen.

**Solución:** Actualizar cada N frames usando el operador módulo `%`

```
frame: 1  2  3  4  5  6  7  8  9  [10] 11 12 ...
                                    ↑
                              frameCount % 10 === 0
                              → actualizar stats aquí
```

### 📝 Pasos

1. Agregar IDs funcionales al HTML de stats (`star-count`, `fps-count`, `mouse-pos`)
2. Crear función `updateStats()` unificada
3. Usar `frameCount % 10 === 0` para limitar las actualizaciones
4. Agregar fricción `vx *= 0.98` a las estrellas nuevas

### Código — `Script completo — Versión Final`

```javascript
<script>
    // ==========================================
    // BLOQUE 5: Versión Final Optimizada
    // ==========================================
    let stars = [];
    let starColor;
    let currentColor;

    function setup() {
        let canvas = createCanvas(windowWidth, windowHeight);
        canvas.parent('p5-container');

        starColor = color(222, 183, 255);
        currentColor = starColor;

        for (let i = 0; i < 100; i++) {
            stars.push(new Star());
        }

        updateStarCount();   // Mostrar 100 al inicio
    }

    function draw() {
        background(23, 13, 44, 30);

        // Actualizar estrellas (iteración inversa para eliminar)
        for (let i = stars.length - 1; i >= 0; i--) {
            stars[i].update();
            stars[i].display();

            if (stars[i].isDead()) {
                stars.splice(i, 1);
            }
        }

        // Cursor
        noCursor();
        noFill();
        stroke(currentColor);
        strokeWeight(2);
        circle(mouseX, mouseY, 40);
        fill(currentColor);
        noStroke();
        circle(mouseX, mouseY, 20);

        // ==========================================
        // OPTIMIZACIÓN: Actualizar stats cada 10 frames
        // ==========================================
        if (frameCount % 10 === 0) {
            updateStats();
            updateStarCount();
        }
    }

    function mousePressed() {
        for (let i = 0; i < 5; i++) {
            stars.push(new Star(mouseX, mouseY, true));
        }
    }

    function changeColor(hexColor) {
        let newColor = color(hexColor);
        currentColor = newColor;
        starColor = newColor;
        for (let star of stars) {
            star.col = newColor;
        }
    }

    // ==========================================
    // NUEVO: Función unificada de stats
    // ==========================================
    function updateStats() {
        let fpsElement = document.getElementById('fps-count');
        if (fpsElement) {
            fpsElement.textContent = Math.floor(frameRate());
        }

        let posElement = document.getElementById('mouse-pos');
        if (posElement) {
            posElement.textContent = mouseX + ',' + mouseY;
        }
    }

    function updateStarCount() {
        let countElement = document.getElementById('star-count');
        if (countElement) {
            countElement.textContent = stars.length;
        }
    }

    function windowResized() {
        resizeCanvas(windowWidth, windowHeight);
    }

    class Star {
        constructor(x, y, isNew = false) {
            if (isNew) {
                this.x = x + random(-20, 20);
                this.y = y + random(-20, 20);
                this.vx = random(-3, 3);
                this.vy = random(-3, 3);
                this.life = 255;
                this.isNew = true;
            } else {
                this.x = random(width);
                this.y = random(height);
                this.vx = 0;
                this.vy = 0;
                this.life = -1;
                this.isNew = false;
            }

            this.size = random(0.5, 3);
            this.baseAlpha = random(100, 255);
            this.alpha = this.baseAlpha;
            this.twinkleSpeed = random(0.02, 0.08);
            this.twinkleOffset = random(TWO_PI);
            this.col = starColor;
        }

        update() {
            if (this.isNew) {
                this.x += this.vx;
                this.y += this.vy;
                this.life -= 3;
                this.alpha = this.life;

                // MEJORA: Fricción para movimiento más natural
                // Multiplicar velocidad por 0.98 = reducir 2% cada frame
                this.vx *= 0.98;
                this.vy *= 0.98;

            } else {
                this.twinkleOffset += this.twinkleSpeed;
                this.alpha = this.baseAlpha + sin(this.twinkleOffset) * 50;
                this.alpha = constrain(this.alpha, 50, 255);
            }
        }

        display() {
            if (this.alpha <= 0) return;

            noStroke();
            fill(red(this.col), green(this.col), blue(this.col), this.alpha);
            circle(this.x, this.y, this.size);

            if (this.size > 2 || this.isNew) {
                fill(red(this.col), green(this.col), blue(this.col), this.alpha * 0.3);
                circle(this.x, this.y, this.size * 3);
            }
        }

        isDead() {
            return this.isNew && this.life <= 0;
        }
    }
</script>
```

### ✅ Verificación Final del Proyecto

- [ ] FPS se mantiene estable cerca de 60
- [ ] La posición X,Y del mouse se actualiza suavemente
- [ ] El contador refleja el número real de estrellas activas
- [ ] Las estrellas nuevas desaceleran gradualmente (efecto de fricción)
- [ ] Todo el sistema es estable y no consume memoria infinitamente

---

## 📋 Cheatsheet de Referencia

_Guía rápida para consultar durante el desarrollo_

---

### 1. Estructura HTML Base

```html
<!-- Tailwind CDN -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- Configuración del tema -->
<script>
	tailwind.config = {
		darkMode: 'class',
		theme: {
			extend: {
				colors: {
					surface: '#170d2c',
					primary: '#deb7ff',
				},
			},
		},
	};
</script>

<!-- Contenedor p5.js — siempre DETRÁS del contenido -->
<div id="p5-container" class="fixed inset-0 -z-10"></div>

<!-- Contenido encima del canvas -->
<main class="relative z-10">...</main>

<!-- p5.js al final del body -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.min.js"></script>
```

---

### 2. Estructura p5.js Base

```javascript
let miVariable;

function setup() {
	let canvas = createCanvas(windowWidth, windowHeight);
	canvas.parent('p5-container');
	// Inicialización (se ejecuta una vez)
}

function draw() {
	background(r, g, b, alpha);
	// Dibujar — se ejecuta ~60 veces/segundo
}

function windowResized() {
	resizeCanvas(windowWidth, windowHeight);
}

function mousePressed() {
	// Evento de click del mouse
}
```

---

### 3. Patrón de Clase para Partículas

```javascript
class Particula {
	constructor(x, y) {
		this.x = x || random(width);
		this.y = y || random(height);
		this.vx = random(-2, 2);
		this.vy = random(-2, 2);
		this.life = 255;
		this.col = color(255);
	}

	update() {
		this.x += this.vx;
		this.y += this.vy;
		this.life -= 2;
	}

	display() {
		fill(red(this.col), green(this.col), blue(this.col), this.life);
		noStroke();
		circle(this.x, this.y, 10);
	}

	isDead() {
		return this.life <= 0;
	}
}
```

| Operación        | Código                                   |
| ---------------- | ---------------------------------------- |
| Crear            | `let p = new Particula(mouseX, mouseY);` |
| Guardar          | `particulas.push(p);`                    |
| Actualizar       | `for (let p of particulas) p.update();`  |
| Eliminar muertas | `if (p.isDead()) array.splice(i, 1);`    |

---

### 4. Comunicación Bidireccional

**HTML → p5.js** (vía `onclick`)

```html
<!-- En HTML -->
<button onclick="miFuncion('parametro')">Click</button>
```

```javascript
// En p5.js — función global accesible desde HTML
function miFuncion(valor) {
	console.log(valor);
	// Actualizar variables del sketch
}
```

**p5.js → HTML** (vía DOM)

```javascript
// Leer elemento
let el = document.getElementById('mi-id');

// Modificar texto
el.textContent = 'nuevo texto';

// Modificar estilo dinámicamente
el.style.color = 'red';
```

---

### 5. Checklist de Optimización

| ✅ Hacer                                    | ❌ Evitar                       |
| ------------------------------------------- | ------------------------------- |
| Usar `canvas.parent('id')`                  | Crear canvas sin `parent()`     |
| Iterar al revés al eliminar con `splice`    | Modificar el DOM cada frame     |
| Limitar updates de DOM con `frameCount %`   | Dejar objetos sin eliminar      |
| Usar `background(r,g,b, alpha)` para estela | Arrays que crecen infinitamente |
| Reciclar objetos cuando sea posible         | Olvidar `windowResized()`       |

---

### 6. Colores de Referencia

| Nombre         | HEX       | RGB             | Uso             |
| -------------- | --------- | --------------- | --------------- |
| Cosmos Surface | `#170d2c` | `23, 13, 44`    | Fondo oscuro    |
| Cosmos Primary | `#deb7ff` | `222, 183, 255` | Estrella morada |
| Rojo Coral     | `#ff6b6b` | `255, 107, 107` | Botón Rojo      |
| Teal           | `#4ecdc4` | `78, 205, 196`  | Botón Teal      |
| Amarillo       | `#ffe66d` | `255, 230, 109` | Botón Amarillo  |

---

_Guía generada a partir de `p5js_tailwind.html` • Diseño Web Interactivo_
