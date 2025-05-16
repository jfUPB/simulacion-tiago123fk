# Consolidando la experiencia audiovisual generativa
### Conexión sonido-visión

Una de las cosas que más me enfoqué en este proyecto fue lograr que la visualización realmente respondiera al audio de forma musical, no solo decorativa. Usé la amplitud general para controlar el número de partículas y el `FFT` para modular color, distorsión, velocidad y rayos de luz. Siento que logré una sincronización efectiva entre las frecuencias del sonido y la imagen.


Lo más difícil fue encontrar el balance entre sensibilidad y estabilidad. Si todo respondía demasiado rápido, se sentía caótico. Si era muy lento, perdía el sentido de sincronía. Tuve que ajustar bien los `map()` y los multiplicadores para que cada elemento reaccionara como yo quería.

### Generatividad vs. Control

Este proyecto también me retó a pensar cómo hacer una obra que no se repitiera pero que no fuera puro caos. Usé aleatoriedad controlada para cambiar automáticamente de modos visuales y paletas cada cierto tiempo, y también permití interacción manual para alterar el color y la densidad del fondo.


Además, el uso de rotación, glitch, simetría, ruido Perlin y distintos tipos de partículas hace que cada ejecución sea diferente, incluso con la misma canción. Al mismo tiempo, los elementos están controlados por el sonido, así que nunca se pierde la coherencia.


Ese balance entre responder al audio (control) y ser impredecible (generatividad) fue uno de los aspectos que más disfruté diseñar.

### Integración de conceptos del curso

Durante este proyecto final pude integrar prácticamente **todo lo aprendido**:

-   **Sistemas de partículas:** controlados por gravedad, energía y vida útil.
    
-   **Fuerzas:** aplicadas a cada partícula para simular movimiento físico.
    
-   **Ruido Perlin:** para deformar el paisaje y darle organicidad.
    
-   **Aleatoriedad controlada:** en rotaciones, modos, colores y trayectorias.
    
-   **Interacción:** mouse y teclado para modificar el estado del sistema en tiempo real.
    
-   **Visualización dinámica y no repetitiva:** gracias a todos los factores anteriores.


### Desafíos con p5.sound

La librería `p5.sound` fue poderosa pero no tan sencilla. Al principio me costó entender cómo funcionaban , `amplitude` y `FFT` y no solo en este trabajo en los otros también, y también cómo sacarles provecho sin sobrecargar el sistema.


Tuve que ajustar mucho los valores de energía y limitar las partículas con `constrain()` porque en los momentos de alto volumen el sketch se pegaba. También aprendí que `createFileInput()` es útil para no depender de archivos locales fijos.

### Resultado final y proyección

El resultado final está muy cerca de mi concepto original: una visualización generativa, tribal, cósmica y psicodélica que reacciona a la canción _Crusade_. Logré simular una especie de **ritual audiovisual**, con un volcán que escupe energía al ritmo de la música, y un entorno que vibra con cada frecuencia.


Lo que más me enorgullece es que logré unir sonido, visual y código en un solo sistema que se siente completo, potente y único cada vez que se ejecuta.

Si tuviera más tiempo, me gustaría:

-   Agregar **agentes inteligentes** o criaturas que “bailen” con el beat.
    
-   Incluir **flow fields** para darle más profundidad a las trayectorias.
    
-   Permitir usar el **micrófono** como entrada alternativa.
