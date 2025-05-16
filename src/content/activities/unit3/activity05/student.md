# ¿Y qué relación tiene esto de las leyes de Newton con al arte generativo?

### ¿Qué problema tiene este planteamiento?

El problema con la implementación dada es que la aceleración se sobrescribe en cada llamada a `applyForce()`.  


```js
applyForce(force) { this.acceleration = force; //Esto borra cualquier aceleración anterior }
```


Esto significa que si aplicamos primero el viento (`wind`) y luego la gravedad (`gravity`), la aceleración final del objeto será **solo la gravedad**, ya que la última llamada a `applyForce()` sustituye la aceleración en lugar de acumular ambas fuerzas.


### ¿Qué solución propongo?
La solución correcta es sumar todas las fuerzas en cada frame en lugar de sobrescribir la aceleración. Para esto, en `applyForce()` debemos agregar la fuerza en lugar de asignarla directamente.


```js
applyForce(force) { this.acceleration.add(force); //Acumula las fuerzas en lugar de reemplazarlas
}
```


Esto permite que todas las fuerzas aplicadas en el frame actual contribuyan a la aceleración total del objeto antes de actualizar su movimiento.

### ¿Cómo lo implementaría en p5.js?
-   Se definen las fuerzas (`gravity` y `wind`).
-   Se aplican ambas fuerzas con `applyForce()`, que ahora suma las fuerzas en lugar de sobrescribirlas.
-   Se actualiza el objeto, sumando la aceleración a la velocidad y la velocidad a la posición.
-   Se resetea la aceleración con `this.acceleration.mult(0);` para que en el siguiente frame se acumulen nuevas fuerzas desde cero.


**Código**



```js
let mover;

function setup() {
  createCanvas(640, 360);
  mover = new Mover();
}

function draw() {
  background(255);
  
  // Definimos fuerzas externas
  let gravity = createVector(0, 0.2); // Simula la gravedad
  let wind = createVector(0.1, 0); // Simula el viento
  
  // Aplicamos las fuerzas al objeto
  mover.applyForce(gravity);
  mover.applyForce(wind);
  
  // Actualizamos y mostramos el objeto
  mover.update();
  mover.checkEdges();
  mover.show();
}

class Mover {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
  }

  applyForce(force) {
    this.acceleration.add(force); //  Acumulamos las fuerzas
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    
    // Reseteamos la aceleración para el siguiente frame
    this.acceleration.mult(0);
  }

  checkEdges() {
    if (this.position.y > height) {
      this.position.y = height;
      this.velocity.y *= -0.8; // Rebote con pérdida de energía
    }
  }

  show() {
    fill(0);
    ellipse(this.position.x, this.position.y, 20, 20);
  }
}

```
