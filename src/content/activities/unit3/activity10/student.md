# Modelando fuerzas
### Descripción del Proyecto: Simulación de Fuerzas con Interacción y Música

Este proyecto es una simulación interactiva que combina principios físicos con visualización de audio para crear una experiencia dinámica y envolvente. La idea principal fue modelar diferentes fuerzas como fricción, resistencia del aire y atracción gravitacional y hacer que reaccionen tanto a la música en tiempo real como a la interacción del usuario.


La simulación genera un conjunto de partículas que se mueven en el espacio y responden a varias fuerzas. **La fricción** se aplica cuando las partículas tocan el suelo, reduciendo su velocidad gradualmente. **La resistencia del aire** desacelera las partículas en movimiento, simulando la pérdida de energía debido al entorno. **La atracción gravitacional**, inicialmente fija en el centro, ahora es controlada por el usuario con el cursor, permitiendo mover el punto de atracción y experimentar con la dinámica del sistema.


Para hacer la simulación aún más reactiva, se incorporó un análisis de audio en tiempo real usando `p5.FFT()`. Esto permite que las partículas cambien de tamaño, color y movimiento según la intensidad de los bajos, medios y agudos de la música. Por ejemplo, los bajos aumentan la gravedad y dispersan las partículas, los medios afectan la resistencia del aire y los agudos modifican la fricción.


En conclusión, este proyecto explora la relación entre la física y la música en un entorno interactivo, ofreciendo una experiencia visual en la que los usuarios pueden manipular la fuerza de atracción con el cursor y observar cómo los elementos gráficos reaccionan de manera dinámica al sonido. La combinación de estos elementos crea una simulación rica en movimiento y variaciones, proporcionando tanto un ejercicio de modelado físico como una pieza visual inmersiva.


En lugar de crear tres simulaciones separadas para modelar **fricción, resistencia del aire y atracción gravitacional**, decidí combinarlas en una sola visualización interactiva. Esto permitió integrar todas las fuerzas en un mismo entorno y hacer que reaccionaran no solo entre ellas, sino también a la música y a la interacción del usuario. Al agregar el análisis de audio en tiempo real, logré que las partículas respondieran a los diferentes rangos de sonido, mientras que la atracción gravitacional ahora se controla con el cursor.

### Código
```js
// Visualización interactiva con fricción, resistencia del aire y atracción gravitacional basada en música

let particles = [];
let attractor;
let sound;
let fft;
let soundLevel = 0.5; // Nivel de audio procesado

function preload() {
  sound = loadSound('Nokia.mp3'); // Carga un archivo de audio (reemplaza con el tuyo)
}

function setup() {
  createCanvas(640, 360);
  sound.setVolume(0.7);
  fft = new p5.FFT(); // Análisis de audio
  sound.play(); // Reproduce la música
  
  attractor = new Attractor(); // Punto de atracción central
  for (let i = 0; i < 50; i++) {
    particles.push(new Particle(random(width), random(height), random(4, 8))); // Partículas más grandes
  }
}

function draw() {
  background(20, 20, 30, 50); // Deja rastros sutiles para mejorar la sensación de movimiento
  
  attractor.update(mouseX, mouseY); // Mueve el atractor con el cursor
  attractor.show();
  
  let spectrum = fft.analyze();
  let bass = fft.getEnergy('bass');
  let mid = fft.getEnergy('mid');
  let treble = fft.getEnergy('treble');
  
  soundLevel = map(bass, 0, 255, 1, 4); // Aumenta el impacto de la gravedad
  let airResistanceLevel = map(mid, 0, 255, 0.02, 0.1);
  let frictionLevel = map(treble, 0, 255, 0.05, 0.2);
  let particleSize = map(bass, 0, 255, 6, 20); // Partículas más grandes con el sonido
  
  for (let particle of particles) {
    // Fuerza de gravedad ajustada según la música
    let gravity = createVector(0, 0.15 * particle.mass * soundLevel);
    // Resistencia del aire, más fuerte con velocidades altas
    let airResistance = particle.velocity.copy().mult(-airResistanceLevel * particle.velocity.mag());
    // Atracción al punto central (ahora movible)
    let attraction = attractor.attract(particle);
    
    // Aplicar las fuerzas a las partículas
    particle.applyForce(gravity);
    particle.applyForce(airResistance);
    particle.applyForce(attraction);
    
    if (particle.isOnSurface()) {
      // Aplicar fricción solo cuando tocan el suelo
      let friction = particle.velocity.copy().mult(-frictionLevel);
      particle.applyForce(friction);
    }
    
    // Nueva idea: Dispersión de partículas cuando hay bajos fuertes
    if (bass > 180) {
      let explosion = p5.Vector.random2D().mult(random(1, 3) * soundLevel);
      particle.applyForce(explosion);
    }
    
    particle.update();
    particle.checkEdges();
    particle.show(particleSize, bass, treble);
  }
}

class Particle {
  constructor(x, y, m) {
    this.mass = m;
    this.position = createVector(x, y);
    this.velocity = createVector(0, 0);
    this.acceleration = createVector(0, 0);
  }
  applyForce(force) {
    let f = force.copy().div(this.mass);
    this.acceleration.add(f);
  }
  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }
  checkEdges() {
    if (this.position.y > height) {
      this.position.y = height;
      this.velocity.y *= -0.8;
    }
  }
  isOnSurface() {
    return this.position.y >= height - 1;
  }
  show(size, bass, treble) {
    // Colores dinámicos según la música
    let colorR = map(bass, 0, 255, 100, 255);
    let colorB = map(treble, 0, 255, 100, 255);
    fill(colorR, 100, colorB, 150);
    noStroke();
    ellipse(this.position.x, this.position.y, size);
  }
}

class Attractor {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.mass = 30;
  }
  // Permite mover el atractor con el cursor
  update(x, y) {
    this.position.set(x, y);
  }
  attract(particle) {
    let force = p5.Vector.sub(this.position, particle.position);
    let distance = constrain(force.mag(), 5, 50);
    force.normalize();
    let strength = (this.mass * particle.mass * soundLevel) / (distance * distance);
    force.mult(strength);
    return force;
  }
  show() {
    fill(255, 100, 100, 200);
    ellipse(this.position.x, this.position.y, this.mass * 2);
  }
}

```

[Link del proyecto](https://editor.p5js.org/tiago123fk/sketches/QBwXzaP-v)


