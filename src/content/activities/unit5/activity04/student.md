# Consolidación de lo aprendido
### 1. ¿Cómo se gestiona la creación y la desaparición de las partículas y cómo se gestiona la memoria?

Durante esta unidad, entendí que la creación de partículas normalmente se hace dentro del `draw()`, añadiendo nuevas instancias a un arreglo que las contiene. En mi proyecto, se crean dependiendo de la energía de la música, lo que le da un comportamiento más orgánico. Por otro lado, cada partícula tiene una propiedad de vida (`lifespan`) que se va reduciendo en cada frame. Cuando esa vida llega a cero, la partícula se elimina del arreglo usando `splice()`, lo que ayuda a que no se acumulen en memoria.

### 2. ¿Cómo se aplica el marco de movimiento motion 101 en los sistemas de partículas que analizaste en la actividad anterior?

Aplicar fuerzas, actualizar, mostrar. En mi caso, cada partícula primero recibe una fuerza externa (como gravedad, repulsión o atracción según el tipo), luego se actualizan sus velocidades y posiciones usando vectores, y finalmente se dibujan con una función `show()`.

### 3. ¿Cómo se aplican fuerzas externas a los sistemas de partículas que trabajaste en la unidad? ¿Qué fuerzas se aplicaron y cómo están modeladas?

Las fuerzas se aplican como vectores usando `applyForce()`, sumándolas a una aceleración que luego modifica la velocidad. En mi proyecto, apliqué varias, una fuerza de atracción desde el centro (como gravedad invertida), una fuerza de repulsión desde el mouse, y fuerzas internas que cambian dependiendo del volumen y frecuencia de la música. También hay oscilaciones con `sin(frameCount)` que generan movimiento rotacional, lo que también se siente como una fuerza suave que hace girar las partículas.

### 4. ¿Cómo se aplicaste los conceptos de herencia y polimorfismo en los sistemas de partículas que trabajaste en la unidad?

Aplicar herencia me ayudó a no repetir código. Creé una clase base `SpiralParticle` con todo lo común (posición, velocidad, update, etc.), y luego otras clases (`PulseParticle`, `TrailParticle`) heredaron de ahí pero cambiaron su comportamiento con `applyAudio()` y `show()`. Cada subclase tiene una personalidad visual distinta, y eso es justo lo que aprendí del polimorfismo, que puedo usar el mismo método (`update()`, `show()`, `applyAudio()`), pero que se ejecute diferente según el tipo de partícula. Me pareció una forma muy poderosa de organizar código y de construir visuales complejos con estructura clara.

