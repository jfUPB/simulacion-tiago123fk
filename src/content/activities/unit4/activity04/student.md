# Relación con el marco motion 101

### 1. Identifica motion 101. ¿Qué modificación hay que hacer para agregar fuerzas acumulativas?

En la simulación completa (asumiendo que también hay una clase `Mover`), se implementa **Motion 101** con:
```js
this.velocity.add(this.acceleration);
this.position.add(this.velocity);
this.acceleration.mult(0);
```

Cuando se quiere agregar **fuerzas acumulativas**, como la fuerza gravitacional del `Attractor`, se hace lo siguiente:

-   Se crea una función `applyForce(force)` en el objeto que **suma cada fuerza** al vector `acceleration`.
    
-   Cada frame se llama a `applyForce()` una o más veces antes de actualizar el movimiento.
    

**¿Por qué es necesario hacer esta modificación?**  
Porque queremos que todas las fuerzas (gravedad, fricción, atracción, etc.) **se acumulen antes de mover el objeto**, y no se reemplacen entre sí. Esto imita cómo funciona la física en el mundo real.


### 2. Identifica dónde está el Attractor y cambia su color

Ya lo encontraste: el `Attractor` está definido en la clase que compartiste. Su color está en el método `display()`:
```js
if (this.dragging) {
  fill(50);
} else if (this.rollover) {
  fill(100);
} else {
  fill(175, 200); // color por defecto
}
```
**Para cambiar el color**, por ejemplo a rojo claro, modificamos esta línea:
```js
fill(255, 100, 100); // nuevo color del Attractor
```

### 3. ¿Cómo podrías modificar el código para mover el Attractor con el mouse y cambiar su color al pasar por encima?

El código ya tiene los atributos `dragging` y `rollover`, así que solo falta activar esas interacciones con el mouse.


**Dentro de la clase `Attractor`**:
```js
// Verifica si el mouse está sobre el Attractor
rolloverCheck(mx, my) {
  let d = dist(mx, my, this.position.x, this.position.y);
  this.rollover = (d < this.mass);
}

// Inicia el arrastre si el mouse está encima
clicked(mx, my) {
  let d = dist(mx, my, this.position.x, this.position.y);
  if (d < this.mass) {
    this.dragging = true;
    this.dragOffset = p5.Vector.sub(this.position, createVector(mx, my));
  }
}

// Detiene el arrastre
released() {
  this.dragging = false;
}

// Actualiza la posición si está siendo arrastrado
drag(mx, my) {
  if (this.dragging) {
    this.position = createVector(mx, my).add(this.dragOffset);
  }
}
```
### Código completo
```js
let attractor;
let movers = [];

function setup() {
  createCanvas(600, 400);
  attractor = new Attractor();

  for (let i = 0; i < 20; i++) {
    movers[i] = new Mover(random(width), random(height), random(0.5, 3));
  }
}

function draw() {
  background(255);

  attractor.rolloverCheck(mouseX, mouseY);
  attractor.drag(mouseX, mouseY);
  attractor.display();

  for (let mover of movers) {
    let force = attractor.attract(mover);
    mover.applyForce(force);
    mover.update();
    mover.display();
  }
}

function mousePressed() {
  attractor.clicked(mouseX, mouseY);
}

function mouseReleased() {
  attractor.released();
}


// CLASE ATTRACTOR

class Attractor {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.mass = 20;
    this.G = 1;
    this.dragging = false;
    this.rollover = false;
    this.dragOffset = createVector(0, 0);
  }

  attract(mover) {
    let force = p5.Vector.sub(this.position, mover.position);
    let distance = force.mag();
    distance = constrain(distance, 5, 25);
    let strength = (this.G * this.mass * mover.mass) / (distance * distance);
    force.setMag(strength);
    return force;
  }

  rolloverCheck(mx, my) {
    let d = dist(mx, my, this.position.x, this.position.y);
    this.rollover = (d < this.mass);
  }

  clicked(mx, my) {
    let d = dist(mx, my, this.position.x, this.position.y);
    if (d < this.mass) {
      this.dragging = true;
      this.dragOffset = p5.Vector.sub(this.position, createVector(mx, my));
    }
  }

  drag(mx, my) {
    if (this.dragging) {
      this.position = createVector(mx, my).add(this.dragOffset);
    }
  }

  released() {
    this.dragging = false;
  }

  display() {
    ellipseMode(CENTER);
    stroke(0);
    if (this.dragging) {
      fill(50); // color cuando lo estás arrastrando
    } else if (this.rollover) {
      fill(255, 100, 100); // color cuando el mouse pasa encima
    } else {
      fill(175, 200); // color normal
    }
    ellipse(this.position.x, this.position.y, this.mass * 2);
  }
}


// CLASE MOVER

class Mover {
  constructor(x, y, m) {
    this.position = createVector(x, y);
    this.velocity = createVector();
    this.acceleration = createVector();
    this.mass = m;
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  display() {
    stroke(0);
    fill(127, 150);
    ellipse(this.position.x, this.position.y, this.mass * 16);

    // Línea que indica orientación
    let angle = this.velocity.heading();
    let r = this.mass * 8;
    push();
    translate(this.position.x, this.position.y);
    rotate(angle);
    line(0, 0, r, 0);
    pop();
  }
}

```
