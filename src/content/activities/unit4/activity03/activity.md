#### Exploración de conceptos fundamentales

Esta actividad te tomará toda la sesión de la clase y posiblemente parte de la sesión de trabajo 
independiente.

**Enunciado**: vas a iniciar analizando algunas simulaciones que te permitirán comprender y experimentar con los conceptos

1. Es momento de retomar lo que has aprendido en las unidades previas e integrarlo con los nuevos conceptos 
de esta unidad. Observa detenidamente la siguiente simulación:

[Motion 101 con fuerzas](https://editor.p5js.org/juanferfranco/sketches/jebkEAUpR)

- Identifica motion 101. ¿Qué modificación hay que hacer al motion 101 cuando se quiere agregar fuerzas 
acumulativas? Trata de recordar por qué es necesario hacer esta modificación.
- Identifica dónde está el Attractor en la simulación. Cambia el color de este.
- Observa que el Attractor tiene dos atributos this.dragging y this.rollover. Estos atributos 
no se modifican en el código, pero permitirían mover el attractor con el mouse y cambiar su color 
cuando el mouse está sobre él. ¿Cómo podrías modificar el código para que esto funcione? considera 
las funciones que ofrece p5.js para [interactuar con el mouse](https://p5js.org/reference/).

2. Explora otro sistema de coordenadas útil cuando se trabaja con ángulos. Se trata de las coordenadas polares.

[Coordenadas polares](https://editor.p5js.org/juanferfranco/sketches/fE5rCtDS1)

- Observa de nuevo esta parte del código ¿Cuál es la relación entre r y theta con las posiciones x y y? Puedes 
repasar entonces la definición de coordenadas polares y cómo se convierten a coordenadas cartesianas.

``` js
function draw() {
  background(255);
  // Translate the origin point to the center of the screen
  translate(width / 2, height / 2);
  // Convert polar to cartesian
  let x = r * cos(theta);
  let y = r * sin(theta);
  fill(127);
  stroke(0);
  strokeWeight(2);
  line(0, 0, x, y);
  circle(x, y, 48);
  theta += 0.02;
}
```
 
 Modifica la función ``draw()``:

``` js
 function draw() {
  background(255);
  // Translate the origin point to the center of the screen
  translate(width / 2, height / 2);
  let v = p5.Vector.fromAngle(theta);
  fill(127);
  stroke(0);
  strokeWeight(2);
  line(0, 0, x, y);
  circle(v.x, v.y, 48);
  theta += 0.02;
}
```

¿Qué ocurre? ¿Por qué?

Ahora realiza esta modificación:

``` js
 function draw() {
  background(255);
  // Translate the origin point to the center of the screen
  translate(width / 2, height / 2);
  let v = p5.Vector.fromAngle(theta,r);
  fill(127);
  stroke(0);
  strokeWeight(2);
  line(0, 0, v.x, v.y);
  circle(v.x, v.y, 48);
  theta += 0.02;
}
```

- ¿Qué ocurre aquí? ¿Por qué?

3. Ahora te pediré que repases la función sinusoide [aquí](https://es.wikipedia.org/wiki/Sinusoide).

- Recuerda estos conceptos: velocidad angular, frecuencia, periodo, amplitud y fase.
- Realiza una simulación en la que puedas modificar estos parámetros y observar cómo se comporta la función sinusoide.

Por ejemplo, te doy ideas, si juego solo con la fase, mira [este ejemplo](https://editor.p5js.org/juanferfranco/sketches/201gcBvjy).

4. Aplica conceptos de la unidades anteriores tomando como base [esta](https://editor.p5js.org/natureofcode/sketches/b3HpgJa6F) simulación. 
La idea es que la modifiques incluyendo un concepto de la unidad 1 (aleatoriedad) y la unidad 3 (fuerzas).

5. TODO:

ejercicios con estas tres simulaciones:

-Exercise 3.12
- Exercise 3.14
- Exercise 3.15

**Entrega**:    