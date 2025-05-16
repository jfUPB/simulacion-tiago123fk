# Motion 101
### ¿En qué consiste motion 101?
El concepto de **Motion 101** es un marco de trabajo para el movimiento basado en vectores, propuesto en The Nature of Code. En lugar de manipular directamente la posición de un objeto, se define el movimiento usando vectores de posición, velocidad y aceleración, logrando un comportamiento más realista y flexible.


**Principios clave de Motion 101:**

1.  **Posición (`position`)**: Es el punto donde se encuentra el objeto en un instante de tiempo.
2.  **Velocidad (`velocity`)**: Es el cambio en la posición con el tiempo (dirección y rapidez).
3.  **Aceleración (`acceleration`)**: Es el cambio en la velocidad con el tiempo (fuerzas externas).


 La idea principal es actualizar la posición sumando la velocidad y actualizar la velocidad sumando la aceleración.

### Ejemplo código 
```js
let mover;

function setup() {
  createCanvas(400, 400);
  mover = new Mover();
}

function draw() {
  background(220);
  mover.update();
  mover.display();
}

class Mover {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0.01, 0.01); // Aceleración constante
  }

  update() {
    this.velocity.add(this.acceleration); // La aceleración cambia la velocidad
    this.position.add(this.velocity); // La velocidad cambia la posición
  }

  display() {
    fill(50, 100, 255);
    ellipse(this.position.x, this.position.y, 20, 20);
  }
}

```


### Explicación del Código

1.  **Definimos un objeto `Mover` con tres vectores:**
    
    -   `position`: Ubicación del objeto.
    -   `velocity`: Velocidad del objeto (cambia la posición).
    -   `acceleration`: Aceleración del objeto (cambia la velocidad).
2.  **En cada `draw()`, el objeto se mueve:**
    
    -   Primero, se le suma la aceleración a la velocidad, la velocidad cambia con el tiempo.
    -   Luego, se le suma la velocidad a la posición, el objeto se mueve de forma progresiva.
