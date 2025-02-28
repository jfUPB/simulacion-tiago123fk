# Materialización
### Código


 **Motion 101 + Sonido + Partículas Dinámicas**


 ```js
let particles = [];
let song;
let fft;
let isPlaying = false;

function preload() {
  song = loadSound('EyeJoe.mp3'); // Carga el archivo de audio
}

function setup() {
  createCanvas(600, 600);
  fft = new p5.FFT();

  for (let i = 0; i < 300; i++) { // Más partículas desde el inicio
    particles.push(new Particle(random(width), random(height)));
  }
}

function draw() {
  background(10, 10, 30, 25);

  let spectrum = fft.analyze(); // Obtener espectro de frecuencias
  let bass = fft.getEnergy("bass"); // Obtener energía de los bajos
  let mid = fft.getEnergy("mid"); // Frecuencias medias
  let treble = fft.getEnergy("treble"); // Frecuencias altas

  // Agregar partículas progresivamente
  if (frameCount % 5 === 0) {
    particles.push(new Particle(random(width), random(height)));
  }

  // Limitar la cantidad de partículas para optimizar rendimiento
  if (particles.length > 500) {
    particles.splice(0, 1);
  }

  for (let p of particles) {
    let force = p5.Vector.random2D().mult(bass / 100); // Movimiento según bajos
    p.applyForce(force);
    p.update(mid, treble); // Se actualiza con frecuencias medias y altas
    p.show();
  }
}

// Iniciar o pausar la canción al hacer clic
function mousePressed() {
  if (!isPlaying) {
    song.play();
    isPlaying = true;
  } else {
    song.pause();
    isPlaying = false;
  }
}

class Particle {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = p5.Vector.random2D().mult(random(1, 3));
    this.acceleration = createVector(0, 0);
    this.size = 8;
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update(mid, treble) {
    this.velocity.add(this.acceleration);
    this.velocity.limit(5);
    this.position.add(this.velocity);
    this.acceleration.mult(0);

    // Tamaño cambia con los bajos de la música
    this.size = map(fft.getEnergy("bass"), 0, 255, 8, 25);

    // Color cambia con las frecuencias altas
    this.color = color(map(treble, 0, 255, 100, 255), 100, 255);
  }

  show() {
    noStroke();
    fill(this.color);
    ellipse(this.position.x, this.position.y, this.size, this.size);
  }
}
```

### Explicación de la Implementación


 **Cada partícula sigue Motion 101:**


-   **Aceleración, Velocidad, Posición.**
-   La aceleración es influenciada por la energía del sonido (bass, mid, treble).


 **Interactividad:**


-   **Las partículas reaccionan a la música**, cambiando tamaño, velocidad y color.
-   **El usuario puede pausar o reproducir la música con un clic.**


 **Optimización:**


-   Se agregan nuevas partículas con el tiempo.
-   Se eliminan partículas viejas para mejorar el rendimiento.


### Conclusión Final

Esta aplicación cumple con Motion 101, ya que el movimiento de las partículas está basado en posición, velocidad y aceleración, influenciadas por la música y la interacción del usuario.
