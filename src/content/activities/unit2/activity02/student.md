# Repaso
### Enunciado
 [Ejercicio 1.1](https://natureofcode.com/vectors/#exercise-11)


Toma uno de los ejemplos de caminantes del  [Capítulo 0](https://natureofcode.com/random#section-random)  y conviértelo para usar vectores.


### Solución 
Elegimos este código de caminata aleatoria basado en **The Nature of Code** de Daniel Shiffman porque representa una forma simple pero efectiva de modelar movimientos aleatorios. En la versión original, la posición del caminante se manejaba con variables escalares `x` e `y`, lo que limitaba la flexibilidad del código. Para mejorar su estructura y escalabilidad, realizamos una modificación donde reemplazamos estas variables por un **vector `p5.Vector`**, lo que facilita la manipulación del movimiento en dos dimensiones. Ahora, en lugar de actualizar `x` e `y` manualmente, utilizamos el método `.add(step)`, permitiendo una implementación más eficiente y adaptable. Esta modificación sienta las bases para futuras mejoras, como la integración de aceleración, velocidades variables o patrones de movimiento más avanzados.

```js
// The Nature of Code
// Daniel Shiffman - Modificación para usar p5.Vector

let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    // Usar un vector para la posición en lugar de variables escalares
    this.position = createVector(width / 2, height / 2);
  }

  show() {
    stroke(0);
    point(this.position.x, this.position.y);
  }

  step() {
    // Crear un vector de dirección inicializado en (0,0)
    let step = createVector(0, 0);

    const choice = floor(random(4));
    if (choice == 0) {
      step.x = 1;  // Mover a la derecha
    } else if (choice == 1) {
      step.x = -1; // Mover a la izquierda
    } else if (choice == 2) {
      step.y = 1;  // Mover hacia abajo
    } else {
      step.y = -1; // Mover hacia arriba
    }

    // Aplicar el desplazamiento sumando el vector step a la posición
    this.position.add(step);
  }
}

```
