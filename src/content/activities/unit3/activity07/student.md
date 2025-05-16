# En mi mundo los pixeles si tienen masa
### ¿Qué problema tiene este planteamiento?

El problema está en esta línea del código dentro de `applyForce(force)`:

```js
 force.div(10);
```

Aquí estamos dividiendo `force` entre 10 para representar la masa del objeto, lo cual está bien en términos físicos, ya que: [*a =F/M*] Sin embargo, el error radica en que `force` es un objeto de la clase `p5.Vector` y se pasa por referencia, no por valor.


**¿Qué significa esto?**  


Cuando modificamos `force` dentro de `applyForce(force)`, estamos alterando el objeto original fuera de la función, lo que afecta todas las fuerzas que aplicamos.


### **¿Qué solución propongo?**

La solución correcta es crear una copia de `force` antes de modificarla. En `p5.js`, se puede hacer usando el método `copy()` para evitar modificar el objeto original.


```js
applyForce(force) {
    let f = force.copy(); //  Crear una copia de la fuerza
    f.div(10); // Ahora dividimos solo la copia
    this.acceleration.add(f); // Acumulamos la fuerza ajustada en la aceleración
}

```
-   Ahora `force.copy()` crea un nuevo vector con los mismos valores de `force`, por lo que la división afecta solo a la copia y no al objeto original.
-   Cada llamada a `applyForce()` ahora usa una versión independiente de la fuerza.


### ¿Cómo lo implementaría en p5.js?

```js
let mover;

function setup() {
  createCanvas(640, 360);
  mover = new Mover(10); // Un objeto con masa = 10
}

function draw() {
  background(255);
  
  let gravity = createVector(0, 0.2); // Simula gravedad
  let wind = createVector(0.1, 0);   // Simula viento
  
  mover.applyForce(wind);
  mover.applyForce(gravity);
  
  mover.update();
  mover.checkEdges();
  mover.show();
}

class Mover {
  constructor(m) {
    this.mass = m;
    this.position = createVector(width / 2, height / 2);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
  }

  applyForce(force) {
    let f = force.copy(); //  Se copia la fuerza para no modificar la original
    f.div(this.mass); // Se divide por la masa correctamente
    this.acceleration.add(f); // Se acumula en la aceleración
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0); // Reset de aceleración en cada frame
  }

  checkEdges() {
    if (this.position.y > height) {
      this.position.y = height;
      this.velocity.y *= -0.8; // Rebote con pérdida de energía
    }
  }

  show() {
    fill(0);
    ellipse(this.position.x, this.position.y, this.mass * 2, this.mass * 2);
  }
}

```
**Solución:** En `applyForce()`, en lugar de modificar `force` directamente, se usa `force.copy()` para trabajar con una copia. Así, la fuerza original permanece intacta.
