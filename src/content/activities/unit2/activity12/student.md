# Análisis de resultados
### Desafíos encontrados

Durante la fase APPLY, tuve que enfrentar varios desafíos al implementar la aplicación interactiva de arte generativo con Motion 101 y análisis de audio.


**Comprender y aplicar Motion 101 correctamente**

-   Al inicio, el concepto de posición, velocidad y aceleración parecía sencillo, pero fue un reto lograr que las partículas reaccionaran de manera fluida y natural a la música.
-   **Solución:** Experimenté con diferentes formas de modificar la aceleración y la velocidad, ajustando los valores en `applyForce()` para mejorar la dinámica del movimiento.

**Integrar correctamente el análisis de audio**

-   Fue difícil lograr que las partículas respondieran de manera perceptible a las diferentes frecuencias del sonido.
-   **Solución:** Ajusté los valores de `fft.getEnergy("bass")`, `fft.getEnergy("mid")` y `fft.getEnergy("treble")`, mapeando estos valores a cambios en tamaño, color y velocidad.

**Optimización del rendimiento con muchas partículas**

-   Al aumentar el número de partículas para mejorar la visualización, el rendimiento bajó.
-   **Solución:** Implementé un sistema que agrega partículas progresivamente y elimina las más antiguas para evitar sobrecarga.


**Problemas con la carga y reproducción del audio**

-   Descubrí que los navegadores modernos bloquean la reproducción automática del audio.
-   **Solución:** Implementé un sistema donde el usuario debe hacer clic para iniciar la canción (`mousePressed()`), lo que resolvió el problema y aparte cargue la canción en p5.js.


### Lecciones aprendidas
**Motion 101 es clave para el movimiento realista**

-   Comprendí que la aceleración afecta la velocidad y la velocidad afecta la posición, y cómo pequeños cambios pueden generar movimientos más orgánicos.

 **El sonido es una gran herramienta para la interacción visual**

-   Aprendí a usar **p5.FFT()** para analizar el audio y mapear diferentes frecuencias en efectos visuales dinámicos.

 **La optimización es crucial en sistemas interactivos**

-   Implementar límites en la cantidad de partículas y usar un fondo con transparencia para crear efecto de "rastro" sin sobrecargar la pantalla fue clave.

 **Siempre es bueno experimentar y ajustar valores**

-   Pequeños cambios en parámetros como `velocity.limit(5);` o `force.setMag(0.1);` pueden hacer una gran diferencia en la fluidez del movimiento.
