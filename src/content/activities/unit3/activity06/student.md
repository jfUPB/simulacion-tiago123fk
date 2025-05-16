#  La fuerza neta debe ser acumulativa

### ¿Por qué multiplicamos la aceleración por cero al final de `update()`?
Cuando trabajamos con fuerzas en una simulación, es importante recordar que la aceleración no es una propiedad acumulativa en el tiempo, a diferencia de la velocidad y la posición. Es decir, en cada frame del programa, la aceleración debe calcularse nuevamente con base en las fuerzas aplicadas en ese instante.


### ¿Qué pasaría si no reiniciamos la aceleración?

Si no multiplicamos la aceleración por cero (`this.acceleration.mult(0);`), la aceleración seguiría acumulándose en cada frame, lo que no representa correctamente la física real. En la vida real:


-   La aceleración es el resultado instantáneo de la suma de fuerzas en cada momento.
-   La velocidad es la que se acumula con el tiempo, no la aceleración.


En términos de código, si no la reseteamos, estaríamos aplicando la misma fuerza una y otra vez en cada frame, causando un comportamiento irreal donde el objeto se acelera indefinidamente sin razón.


### Conclusión

Multiplicar la aceleración por cero al final de `update()` es esencial para que en cada frame la aceleración se reinicie y se vuelva a calcular correctamente con las fuerzas aplicadas en ese instante. De lo contrario, la aceleración seguiría acumulándose de manera irreal y afectaría el movimiento del objeto.


Este pequeño detalle asegura que nuestras simulaciones sigan principios físicos correctos y generen movimientos realistas en arte generativo y visuales interactivos.
