# Interpolamos?

### ¿Cómo funciona lerp()

El método `lerp()` (Linear Interpolation) permite encontrar un punto intermedio entre dos valores o vectores según un porcentaje dado.

### ¿Cómo funciona lerpColor()
El método `lerpColor()` permite hacer una interpolación entre dos colores, creando una transición suave entre ellos.
###    ¿Cómo se dibuja una flecha usando drawArrow()?
El método `drawArrow()` dibuja una flecha a partir de un punto base (`base`) en la dirección de un vector (`vec`).

### Código
```js
let v0, v1, v2;
let t = 0; // Variable para la interpolación

function setup() {
  createCanvas(400, 400);

  // Definir los vértices del triángulo
  v0 = createVector(50, 50);   // Vértice superior izquierdo
  v1 = createVector(350, 50);  // Vértice superior derecho (rojo)
  v2 = createVector(50, 350);  // Vértice inferior izquierdo (verde)
}

function draw() {
  background(200);

  // Interpolación para la flecha oscilante
  let v3 = p5.Vector.lerp(v1, v2, abs(sin(t))); // Oscila entre rojo y verde

  //  Ajustar los colores de la flecha oscilante
  let color1 = color(255, 0, 0);  // Rojo
  let color2 = color(0, 0, 255);  // Azul
  let midColor = lerpColor(color1, color2, abs(sin(t))); // Cambio de azul → morado → rojo

  // Dibujar las flechas principales del triángulo
  drawArrow(v0, v1.copy().sub(v0), color(255, 0, 0)); // Flecha roja (horizontal)
  drawArrow(v0, v2.copy().sub(v0), color(0, 0, 255)); // Flecha azul (vertical)
  drawArrow(v1, v2.copy().sub(v1), color(0, 255, 0)); //  Flecha verde con dirección invertida

  // Dibujar la flecha oscilante
  drawArrow(v0, v3.copy().sub(v0), midColor); // Flecha oscilante entre roja y verde

  t += 0.01; // Controla la velocidad de oscilación
}

function drawArrow(base, vec, myColor) {
  push();
  stroke(myColor);
  strokeWeight(4);
  fill(myColor);
  translate(base.x, base.y);
  line(0, 0, vec.x, vec.y);
  rotate(vec.heading());
  let arrowSize = 10;
  translate(vec.mag() - arrowSize, 0);
  triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
  pop();
}

``` 
### Conclusión

Gracias a la combinación de interpolación de vectores `lerp()`, interpolación de colores `lerpColor()`, y el método `drawArrow()` para dibujar las flechas, logramos una animación fluida donde la flecha oscilante se mueve entre la roja y la verde, cambiando de color de rojo, morado, azul.
