# Hagamos que todo se mueva
### Cambios a realizar

 - La base del triángulo (`v0`) ahora sigue la posición del mouse.
 - La escala de los vectores cambia dependiendo de la distancia del
   mouse al centro de la pantalla.
 - La flecha oscilante sigue funcionando igual, pero ahora se adapta al
   nuevo tamaño dinámico.

### Explicación de la solución

1.  **Hacer que la base (`v0`) siga el mouse**
    
    -   v0 = createVector(mouseX, mouseY);
    -   Ahora el triángulo se mueve con el mouse.
2.  **Escalar el tamaño del triángulo dinámicamente**
    
    -   Se mide la distancia entre el mouse y el centro de la pantalla con dist(mouseX, mouseY, width / 2, height / 2);.
    -   scaleFactor = map(d, 0, width / 2, 0.5, 1.5); ajusta el tamaño dinámicamente.
	- Mantener la oscilación y el cambio de color de la flecha central


### Código
```js
let v0, v1, v2;
let t = 0; // Variable para la interpolación
let scaleFactor = 1; // Factor de escala dinámico

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(200);

  //Actualizar la base del triángulo según la posición del mouse
  v0 = createVector(mouseX, mouseY);

  //Cambiar la escala de los vectores dependiendo de la distancia al centro
  let d = dist(mouseX, mouseY, width / 2, height / 2);
  scaleFactor = map(d, 0, width / 2, 0.5, 1.5); // Ajusta el tamaño de los vectores

  //Definir los otros vértices con la escala ajustada
  v1 = createVector(v0.x + 150 * scaleFactor, v0.y); // Punto derecho (rojo)
  v2 = createVector(v0.x, v0.y + 150 * scaleFactor); // Punto inferior (azul)

  //Interpolación para la flecha oscilante entre rojo y verde
  let v3 = p5.Vector.lerp(v1, v2, abs(sin(t)));

  //Ajustar los colores de la flecha oscilante
  let color1 = color(255, 0, 0);  // Rojo
  let color2 = color(0, 0, 255);  // Azul
  let midColor = lerpColor(color1, color2, abs(sin(t))); // Cambio de rojo → morado → azul

  //Dibujar las flechas principales del triángulo
  drawArrow(v0, v1.copy().sub(v0), color(255, 0, 0)); // Flecha roja (horizontal)
  drawArrow(v0, v2.copy().sub(v0), color(0, 0, 255)); // Flecha azul (vertical)
  drawArrow(v1, v2.copy().sub(v1), color(0, 255, 0)); // Flecha verde (diagonal invertida)

  //Dibujar la flecha oscilante
  drawArrow(v0, v3.copy().sub(v0), midColor); // Flecha oscilante entre roja y verde

  t += 0.02; // Controla la velocidad de oscilación
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
