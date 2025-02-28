#### Conceptos fundamentales

**Enunciado**: 

Analiza las siguientes simulaciones:

1. [Manejo de ángulos](https://editor.p5js.org/juanferfranco/sketches/R1iTVQjzm).

- ¿Qué está pasando en esta simulación? ¿Cuál es la interacción? 
- Nota que en cada frame se está trasladando el origen del sistema de coordenadas al centro de la pantalla. ¿Por qué crees que se hace esto?
- Cuál es la relación entre el sistema de coordenadas y la función `rotate()`.

Nota esta parte del código:

``` javascript
  line(-50, 0, 50, 0);
  stroke(0);
  strokeWeight(2);
  fill(127);
  circle(50, 0, 16);
  circle(-50, 0, 16);
```

Observa que al dibujar los elementos gráficos parece que se está dibujando en la posición `(0, 0)` del sistema de coordenadas. ¿Por qué crees que se hace esto? y ¿Por qué aunque en cada frame se hace lo mismo, los elementos gráficos rotan?

2. [Apuntar en la dirección del movimiento](https://editor.p5js.org/natureofcode/sketches/bZqHGYbRQ).

- Identifica el marco motion 101. ¿Qué es lo que se está haciendo en este marco?

Observa detenidamente este fragmento de código de la simulación:

``` js
  display() {
    let angle = this.velocity.heading();

    stroke(0);
    strokeWeight(2);
    fill(127);
    push();
    rectMode(CENTER);
    translate(this.position.x, this.position.y);
    rotate(angle);
    rect(0, 0, 30, 10);

    pop();
  }
```

- ¿Qué hace la función `heading()`?
- ¿Qué hace la función `push()` y `pop()`? Realiza algunos experimentos para entender su funcionamiento.
- ¿Qué hace rectMode(CENTER)? Realiza algunos experimentos para entender su funcionamiento.
- ¿Cuál es la relación entre el ángulo de rotación y el vector de velocidad? Trata de dibujar en un papel 
el vector de velocidad y cómo se relaciona con el ángulo de rotación y la operación de traslación y rotación.

3. Una vez hayas analizado las simulaciones, crear una simulación de un vehículo que puedas conducir por la pantalla utilizando las teclas de flecha: la flecha izquierda acelera el vehículo hacia la izquierda, y la flecha derecha acelera hacia la derecha. El vehículo tendrá forma triangular y debe apuntar en la dirección en la que se está moviendo actualmente.

**Entrega**:

- Enlace a la simulación en el editor de p5.js.
- Código de la simulación.
- Captura de pantalla de la simulación.