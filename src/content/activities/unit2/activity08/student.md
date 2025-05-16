# Experimenta
### Entendiendo el ejemplo 1.7

Este código simula un objeto en movimiento con velocidad aleatoria, que al salir de la pantalla reaparece en el lado opuesto, generando un efecto de "teletransportación" en los bordes.


 **Componentes clave del código:**

1.  **`this.position`**: Define la posición inicial en un punto aleatorio.
2.  **`this.velocity`**: Define una velocidad aleatoria en ambas direcciones.
3.  **`update()`**: Actualiza la posición del objeto sumando la velocidad.
4.  **`checkEdges()`**: Si el objeto sale de la pantalla, reaparece en el lado opuesto.


 Este comportamiento es típico en videojuegos, donde los objetos no desaparecen sino que reaparecen al otro lado.

### ¿Qué pasa si…?
**Pregunta:** ¿Qué pasa si, en lugar de teletransportarse, el objeto rebota en los bordes como una pelota?


 **Hipótesis (lo que creo que pasará):**

-   En lugar de reaparecer en el lado opuesto, el objeto rebotará cuando toque los bordes.
-   Se verá un movimiento más natural y controlado, como si estuviera dentro de una caja.

 **Modificación en el código:**


-   En vez de teletransportarlo, invertiremos la dirección de la velocidad cuando toque los bordes.


### Código 
```js
class Mover {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = createVector(random(-2, 2), random(-2, 2));
  }

  update() {
    this.position.add(this.velocity);
  }

  show() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    circle(this.position.x, this.position.y, 48);
  }

  checkEdges() {
    if (this.position.x > width || this.position.x < 0) {
      this.velocity.x *= -1; // Invierte la dirección en X
    }
    if (this.position.y > height || this.position.y < 0) {
      this.velocity.y *= -1; // Invierte la dirección en Y
    }
  }
}

// Variables globales
let mover;

function setup() {
  createCanvas(400, 400);
  mover = new Mover();
}

function draw() {
  background(220);
  mover.update();
  mover.checkEdges(); // Detecta los bordes y rebota
  mover.show();
}

```

### ¿Qué pasó realmente?
-   En lugar de desaparecer y reaparecer en el lado opuesto, el objeto rebotó en los bordes.
-   El movimiento se sintió más realista, similar a una pelota que choca contra las paredes.
-   La velocidad cambió de dirección al tocar un borde, pero mantuvo su magnitud.

### Conclusión Final

Este experimento nos ayudó a entender cómo las condiciones de borde afectan el comportamiento de un objeto en movimiento. Dependiendo del contexto, podemos elegir entre teletransportación o rebote para lograr distintos efectos.
