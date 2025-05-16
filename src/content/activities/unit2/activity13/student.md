# Conexión con Diseño de Entretenimiento Digital

### Simulación de movimiento en videojuegos

**Ejemplo concreto:** Movimiento realista en un juego de plataformas.


En videojuegos, especialmente en juegos de plataformas y simulaciones físicas, es fundamental que los personajes y objetos se muevan de manera natural.


**Ejemplo en un juego:**

-   En un juego tipo _Super Mario Bros_, el personaje no se mueve instantáneamente de un punto a otro, sino que acelera y desacelera gradualmente.
-   Se aplican vectores de movimiento para hacer que el personaje reaccione con mayor realismo a las entradas del jugador.


**Código de ejemplo:**

```js
player.velocity.add(player.acceleration);
player.position.add(player.velocity);
```
### Simulación de física en juegos de carreras
**Ejemplo concreto:** Un coche que se mueve con aceleración progresiva y pierde velocidad por fricción.


En los juegos de carreras, los vehículos no se mueven instantáneamente, sino que aceleran y frenan de manera gradual.


**Ejemplo en un juego de carreras:**

-   Cuando un jugador presiona el acelerador, el coche gana velocidad progresivamente en lugar de moverse instantáneamente.
-   Se implementa resistencia del aire y fricción, para que cuando el jugador suela el acelerador, el coche no se detenga inmediatamente sino que disminuya la velocidad de forma natural.


**Ejemplo en código:**

```js
let acceleration = createVector(0.1, 0); // Aceleración hacia la derecha
velocity.add(acceleration); // La velocidad aumenta gradualmente
velocity.mult(0.98); // Simulación de fricción (pierde velocidad con el tiempo)
position.add(velocity); // Se actualiza la posición del coche

```

### Efectos de partículas en explosiones y fuego


**Ejemplo concreto:** Simulación de partículas en explosiones, humo o fuego.


En juegos y animaciones, explosiones, fuego, nieve y polvo se generan con partículas que siguen movimientos realistas.


**Ejemplo en una explosión:**

-   Cada partícula es un vector con dirección y velocidad.
-   Las partículas salen disparadas desde un punto central con direcciones aleatorias y se desaceleran gradualmente por la gravedad.


**Ejemplo en código:**
```js
let explosionForce = p5.Vector.random2D().mult(random(2, 5)); // Partícula en dirección aleatoria
velocity.add(explosionForce);
velocity.add(gravity); // Simulación de gravedad 
position.add(velocity);
```
