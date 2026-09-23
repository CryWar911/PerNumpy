# Simulador del Perceptrón Simple

Página web interactiva que acompaña al cuaderno `Perceptron_Simple.ipynb` de la actividad **"Implementación y simulación del Perceptrón simple desde cero"**. Permite entrenar un Perceptrón de Rosenblatt paso a paso sobre las compuertas lógicas AND, OR y XOR y ver en tiempo real cómo cambian los pesos, el sesgo y la frontera de decisión.

## Archivos

| Archivo | Descripción |
|---|---|
| `Perceptron_Simple.html` | El simulador. Es un solo archivo e incluye el notebook completo con sus gráficas. |
| `Perceptron_Simple.ipynb` | Cuaderno de Jupyter con la implementación en Python/NumPy, los experimentos y el cuestionario. |
| `IMPLEMENTACIÓN Y SIMULACIÓN DEL PERCEPTRÓN SIMPLE DESDE CERO.docx` | Guía de la actividad: objetivos, instrucciones y rúbrica. |

## Cómo abrirlo

1. Haz doble clic en `Perceptron_Simple.html` para abrirlo en cualquier navegador moderno (Chrome, Edge, Firefox).
2. No hace falta instalar Python ni nada más.
3. Se necesita **conexión a internet** para cargar las fórmulas (KaTeX), el resaltado de código (highlight.js), el render del Markdown (marked) y las tipografías. Sin conexión, el simulador funciona igual, pero las fórmulas y el texto del notebook se ven sin formato.

## Pestañas

### 1. Simulador

**Controles**

| Control | Qué hace |
|---|---|
| Compuerta lógica | Elige el problema: AND, OR o XOR. |
| Tasa de aprendizaje η | Barra de 0.01 a 1, con accesos rápidos a 0.01, 0.1, 0.5 y 1. |
| Épocas máximas | Límite de épocas antes de detenerse (por defecto 100, como en el notebook). |
| Inicialización de pesos | *Ceros* (como en la guía) o *Aleatoria*, con semilla configurable. |
| Velocidad | Pasos por segundo de la animación. |

**Botones y atajos de teclado**

| Botón | Atajo | Acción |
|---|---|---|
| ▶ Entrenar / ⏸ Pausa | — | Entrena de forma animada; se puede pausar y reanudar. |
| Paso (1 muestra) | `Espacio` | Procesa una sola muestra del conjunto de entrenamiento. |
| Época completa | `E` | Procesa las 4 muestras de la época actual. |
| ⏭ Al instante | — | Entrena hasta converger o agotar las épocas. |
| ↺ Reiniciar | `R` | Vuelve a los pesos iniciales. |

Cambiar cualquier parámetro reinicia el entrenamiento.

**Paneles**

- **Estado:** avisa si el modelo convergió (verde), si no convergió (rojo) o si sigue entrenando.
- **Indicadores:** época actual, w₁, w₂, b y exactitud sobre las 4 muestras.
- **Frontera de decisión:** plano entre −0.5 y 1.5 con:
  - regiones coloreadas según la clase que predice la neurona;
  - la recta w₁x₁ + w₂x₂ + b = 0 (discontinua) y la frontera anterior (punteada);
  - el vector de pesos **w**, que es normal a la recta y apunta hacia la clase 1;
  - la muestra en proceso rodeada con un círculo y los puntos mal clasificados marcados con ✗.
- **Convergencia:** errores por época. El círculo hueco representa la época en curso.
- **Último paso del algoritmo:** el cálculo con los números reales: z, ŷ, el error e y, si hay error, la actualización de w y b.
- **Tabla de verdad:** x₁, x₂, y, z, ŷ y acierto (✓/✗) para cada entrada.
- **Consola:** los mismos mensajes que imprime el código Python (`Convergencia alcanzada en la época …` / `No convergió en … épocas …`).
- **Código en ejecución:** la clase `Perceptron` original, con las líneas que se ejecutaron en el último paso resaltadas.

**Cuestionario en vivo**

| Pregunta | Contenido |
|---|---|
| 1. Análisis de convergencia | Tabla de épocas y pesos finales para η = 0.01, 0.1 y 0.5 con pesos en cero; además, un promedio sobre 30 semillas con pesos aleatorios. |
| 2. Separabilidad lineal (XOR) | Red de dos capas (OR + NAND → AND) que sí resuelve XOR. |
| 3. Interpretación de pesos | Explicación de w₁, w₂ y el umbral θ = −b a partir de los pesos actuales de la simulación. |

### 2. Teoría

Resumen del fundamento teórico de la guía: suma ponderada, función escalón de Heaviside, regla de actualización de pesos y ecuación de la frontera de decisión.

### 3. Notebook

El cuaderno `Perceptron_Simple.ipynb` completo, en el orden original, con el código, las salidas de texto y las gráficas de matplotlib (In [1] a In [16]).

## Fidelidad con el notebook

- **El código Python no fue modificado.** Se muestra tal cual en la pestaña Notebook y en el panel de código.
- El simulador usa una réplica en JavaScript de la clase `Perceptron`:
  - misma función escalón (`z >= 0 → 1`);
  - misma regla `w += η·e·x`, `b += η·e`;
  - mismo orden de las muestras;
  - misma parada temprana cuando una época termina con 0 errores.
- Como JavaScript y NumPy usan la misma aritmética de punto flotante (IEEE 754), con pesos en cero los resultados son **idénticos** a los del notebook:

| Compuerta | η | Épocas | w | b |
|---|---|---|---|---|
| AND | 0.1 | 4 | [0.2, 0.1] | −0.2 |
| OR | 0.1 | 4 | [0.1, 0.1] | −0.1 |
| XOR | 0.1 | no converge (100) | [−0.1, 0] | 0 |

  También aparece el mismo detalle numérico del notebook: z ≈ −2.78 × 10⁻¹⁷ en la entrada (1, 0) de AND.
- **Única diferencia:** con inicialización aleatoria, el simulador usa su propio generador de números aleatorios (Mulberry32), no el de NumPy. Los pesos iniciales para una misma semilla y los promedios de la tabla de 30 semillas no coinciden exactamente con el notebook, aunque la conclusión es la misma: η = 0.5 converge mucho más rápido que η = 0.01.

## Otras características

- Tema claro y oscuro (botón **◐ Tema**). La elección se recuerda en el navegador.
- Diseño adaptable a computadora, tablet y celular.
- Sin dependencias de instalación: todo el código del simulador está dentro del HTML.
