# Diseño del algoritmo generativo (proceso y outputs)

### 1.Diseño del Proceso Generativo

####  Lógica Central

El algoritmo generativo tiene como núcleo un sistema de partículas ascendentes que emulan erupciones volcánicas cósmicas, moduladas en tiempo real por la música. Las partículas se generan desde un "cráter central" y son deformadas por ruido Perlin y fuerzas que dependen del FFT.

La base se complementa con:
- Un paisaje de montañas generado por curvas de ruido.
- Un cielo estrellado con partículas flotantes.
- Columnas de luz y rayos que se activan según el beat.

#### Técnicas del curso aplicadas

| Técnica                 | Uso en el proyecto |
|------------------------|--------------------|
| **Sistemas de partículas** | Eruptan desde el suelo, modificadas por amplitud y FFT. |
| **Ruido Perlin**        | Deforma las montañas, afecta el flujo del campo visual. |
| **Fuerzas / gravedad**  | Aplicadas a partículas para darles movimiento y reacción. |
| **Aleatoriedad controlada** | Hace que cada visual sea único pero coherente. |



### 2. Inputs y Parámetros Dinámicos

#### Audio

| Input de Audio      | Parámetro Modulado                                |
|---------------------|---------------------------------------------------|
| **Amplitud**         | Número de partículas generadas por frame.         |
|                     | Tamaño y opacidad de las partículas (más volumen = más intensidad). |
| **FFT – Graves**     | Color y glow del cráter volcánico.                |
|                     | Distorsión del centro visual.                     |
| **FFT – Medios**     | Amplitud del ruido Perlin en las montañas.       |
| **FFT – Agudos**     | Velocidad de partículas, aparición de rayos/luz. |

#### 🖱️ Interacción

| Interacción         | Parámetro Modulado                                |
|---------------------|---------------------------------------------------|
| **Mouse X**          | Cambia la paleta de colores (de cálido a frío).  |
| **Mouse Y**          | Controla la densidad del cielo estrellado.       |
| **Tecla V**          | Modo volcánico extremo: se aumentan los valores máximos. |
| **Tecla S**          | Captura de pantalla.                             |



### 3.Naturaleza Generativa (no repetitiva)

Para asegurar que cada visualización sea **única**, incluso con la misma canción:

- Se usa **ruido Perlin** con offsets que cambian con el tiempo.
- El sistema de partículas tiene **semillas aleatorias** para su posición y velocidad.
- Cada ciclo de la visualización introduce **ligeros desajustes controlados** en el color, opacidad y trayectoria.



### 4.Outputs Visuales

| Elemento Visual      | Propiedades Dinámicas Controladas |
|----------------------|-----------------------------------|
| **Partículas volcánicas** | Posición, velocidad, color, tamaño, opacidad (audio + aleatoriedad). |
| **Montañas alienígenas** | Forma, altura y vibración (FFT medios + Perlin noise). |
| **Rayos de energía**  | Frecuencia de aparición, intensidad y dirección (agudos). |
| **Cielo estrellado**  | Número de partículas y brillo (mouseY + ruido). |
| **Cráter / Centro visual** | Glow, distorsión, color dominante (graves). |


