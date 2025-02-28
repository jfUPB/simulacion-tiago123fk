# Experimentando con la aceleración
### Para entender la frase:

> _"El objetivo de la programación del movimiento es encontrar un algoritmo para calcular la aceleración y dejar que el efecto en cascada haga su magia."_

Significa que si definimos correctamente **cómo cambia la aceleración**, la velocidad y la posición del objeto se ajustarán naturalmente.


Esto pasa por que:

 - Velocidad = Velocidad + Aceleración
 - Posición = Posición + Velocidad


### **Aceleración Constante**

Aquí el objeto tiene una aceleración fija, lo que provoca que su velocidad aumente constantemente y el objeto se mueva cada vez más rápido en una dirección.


```js
class Mover {
  constructor() {
    this.position = createVector(50, 50);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0.05, 0.05); // Aceleración constante
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
  }

  show() {
    fill(127);
    ellipse(this.position.x, this.position.y, 20, 20);
  }
}

let mover;

function setup() {
  createCanvas(400, 400);
  mover = new Mover();
}

function draw() {
  background(220);
  mover.update();
  mover.show();
}
```
**¿Qué pasó?** El objeto se mueve más y más rápido en diagonal porque la aceleración aumenta la velocidad constantemente.  Al principio se mueve lento, pero se acelera con el tiempo.


**¿Por qué?**   La velocidad crece de manera lineal porque la aceleración es fija. El objeto no cambia de dirección porque la aceleración siempre apunta a la misma dirección

### Aceleración Aleatoria
Aquí el objeto cambia su aceleración de forma aleatoria en cada fotograma, lo que provoca un movimiento errático e impredecible.


```js
class Mover {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.velocity = createVector(0, 0);
  }

  update() {
    this.acceleration = p5.Vector.random2D().mult(0.2); // Aceleración aleatoria
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
  }

  show() {
    fill(127);
    ellipse(this.position.x, this.position.y, 20, 20);
  }
}

let mover;

function setup() {
  createCanvas(400, 400);
  mover = new Mover();
}

function draw() {
  background(220);
  mover.update();
  mover.show();
}

```


**¿Qué pasó?**  El objeto se mueve de manera errática e impredecible, cambiando de dirección constantemente.  Se parece a una partícula moviéndose aleatoriamente en un fluido.

**¿Por qué?**  La dirección de la aceleración cambia aleatoriamente en cada fotograma, lo que provoca cambios en la velocidad y, por ende, en la posición.  Este comportamiento es útil para simulaciones de partículas o movimiento orgánico.


### Aceleración Hacia el Mouse
Aquí el objeto siempre acelera hacia el cursor, como si fuera atraído por una fuerza gravitacional.


```js
class Mover {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = createVector(0, 0);
  }

  update() {
    let mouse = createVector(mouseX, mouseY);
    let acceleration = p5.Vector.sub(mouse, this.position); // Vector hacia el mouse
    acceleration.setMag(0.2); // Magnitud fija

    this.velocity.add(acceleration);
    this.velocity.limit(5); // Limita la velocidad máxima
    this.position.add(this.velocity);
  }

  show() {
    fill(127);
    ellipse(this.position.x, this.position.y, 20, 20);
  }
}

let mover;

function setup() {
  createCanvas(400, 400);
  mover = new Mover();
}

function draw() {
  background(220);
  mover.update();
  mover.show();
}

```


**¿Qué pasó?**  El objeto se mueve hacia el cursor, primero despacio y luego más rápido a medida que se acerca.   Si pasas el cursor rápido, el objeto tarda un poco en reaccionar antes de seguirlo.


**¿Por qué?**  La aceleración siempre apunta al vector dirección hacia el mouse, causando que el objeto se acelere en esa dirección. Este comportamiento simula la gravedad o atracción de un objeto hacia un punto.


### Conclusión 

El **Motion 101** funciona permitiendo que la aceleración controle la velocidad y la posición. Dependiendo de cómo definamos la aceleración, podemos obtener efectos completamente diferentes, desde un movimiento uniforme hasta una simulación de partículas caótica.
