
# Implementación
### *Crusade: Ritual Cósmico*
### Configuración y análisis de audio

Para esta actividad implementé mi simulación musical generativa utilizando la librería `p5.sound`. Decidí permitir que el usuario suba el archivo de audio desde la ejecución, usando `createFileInput()`. Esto evita problemas con archivos pesados y permite más flexibilidad.


Una vez cargada la canción, utilizo dos herramientas clave de análisis:

-   `p5.Amplitude` para detectar el volumen general del audio.
    
-   `p5.FFT` para extraer las frecuencias (graves, medios, agudos).
    

Estos datos son la base para controlar todos los elementos visuales del sketch.

### Lógica del algoritmo generativo


El corazón del proyecto es un sistema de partículas que simulan **erupciones de un volcán cósmico**. Las partículas se lanzan desde el centro inferior del lienzo, y su comportamiento depende del volumen y la energía en graves:

-   Si el volumen sube, se generan más partículas.
    
-   Si los graves aumentan, las partículas salen con más fuerza y velocidad.
    
-   Los medios deforman las **montañas alienígenas** generadas con `noise`.
    
-   Los agudos generan **rayos de energía** que cruzan la pantalla.
    

Además, implementé **cuatro modos visuales**, que cambian automáticamente cada 200 frames (aproximadamente cada 3–4 segundos):

-  Partículas normales.
    
- Modo glitch (con puntos y vibraciones).
    
- Modo espejo (simetría horizontal).
    
-  Modo rotación con zoom.

### Interacción en tiempo real

El usuario puede modificar la visualización mientras suena la canción:

-   `mouseX` cambia el color dominante del sistema (`colorModeValue`).
    
-   `S`: guarda una imagen del momento visual.
    
-   `Z`: fuerza el cambio de modo visual manualmente.
    
-   `W`: reinicia el temporizador de cambio automático.
    

Para evitar cuelgues o sobrecarga de partículas durante los drops musicales, limité el número de partículas a un **máximo de 150 por frame** usando `constrain()`. También controlo el total de partículas eliminando las que ya murieron (`lifetime`).

### Resultado final y reflexión

El resultado es una visualización oscura, psicodélica y poderosa que responde con precisión al carácter épico y ritual de la canción _Crusade_. La obra no es repetitiva gracias al uso de aleatoriedad controlada, rotación, cambios de paleta y la dinámica de audio en tiempo real.


Cada ejecución es diferente. Hay elementos que el usuario puede controlar (como el color ), pero también decisiones generativas que cambian cada pocos segundos, lo cual garantiza frescura y unicidad constante.


Esta actividad me permitió integrar todo lo aprendido simulación física, partículas, análisis de sonido, interacción, diseño generativo, ritmo visual, control del tiempo y de la memoria del sistema. Siento que es un cierre ideal para el curso.

### Código

```js
let sound, fft, amplitude;
let particles = [];
let stars = [];
let colorModeValue;
let visualMode;
let starDensity;
let fileInput;
let ready = false;
let palettes = [
  [300, 50, 100],
  [200, 80, 100],
  [0, 100, 100],
  [120, 100, 100]
];
let currentPalette = 0;
let frameTrigger = 0;

function setup() {
  createCanvas(windowWidth, windowHeight);
  colorMode(HSB);

  fileInput = createFileInput(handleFile);
  fileInput.position(20, 20);

  fft = new p5.FFT();
  amplitude = new p5.Amplitude();

  colorModeValue = 0;
  starDensity = 100;
  visualMode = Math.floor(random(4));

  for (let i = 0; i < 300; i++) {
    stars.push(createVector(random(width), random(height)));
  }

  textAlign(CENTER);
  textSize(20);
  fill(255);
  text('Selecciona la canción .mp3 para comenzar', width / 2, height / 2);
}

function handleFile(file) {
  if (file.type === 'audio') {
    loadSound(file.data, (loadedSound) => {
      sound = loadedSound;
      ready = true;
      fileInput.hide();
    });
  } else {
    alert("Por favor selecciona un archivo de audio.");
  }
}

function draw() {
  if (!ready || !sound.isPlaying()) return;

  background(0, 0.1);

  let vol = amplitude.getLevel();
  let spectrum = fft.analyze();
  let bass = fft.getEnergy("bass");
  let mid = fft.getEnergy("mid");
  let treble = fft.getEnergy("treble");

  if (frameCount - frameTrigger > 200) {
    visualMode = Math.floor(random(4));
    currentPalette = Math.floor(random(palettes.length));
    frameTrigger = frameCount;
  }

  // Fondo estrellado
  noStroke();
  fill(0, 0, 100, 0.3);
  for (let i = 0; i < starDensity; i++) {
    let s = stars[i % stars.length];
    ellipse(s.x, s.y, random(1, 3));
  }

  // Montañas deformadas
  stroke(200, 50, 100);
  noFill();
  beginShape();
  for (let x = 0; x < width; x += 10) {
    let y = noise(x * 0.005, frameCount * 0.005) * height / 2;
    let offset = map(mid, 0, 255, -100, 100);
    vertex(x, y + offset + height / 2);
  }
  endShape();

  // Partículas del volcán
 let numParticles = constrain(vol * 400, 0, 150); // nunca más de 150
for (let i = 0; i < numParticles; i++) {
  particles.push(new Particle(width / 2, height - 50, bass));
}

  for (let i = particles.length - 1; i >= 0; i--) {
    let p = particles[i];
    p.update();

    if (visualMode === 0) p.show();
    else if (visualMode === 1) p.showGlitch();
    else if (visualMode === 2) {
      push();
      translate(width, 0);
      scale(-1, 1);
      p.show();
      pop();
    } else if (visualMode === 3) {
      push();
      translate(width / 2, height / 2);
      scale(0.8);
      rotate(frameCount * 0.002);
      translate(-width / 2, -height / 2);
      p.show();
      pop();
    }

    if (p.finished()) particles.splice(i, 1);
  }

  // Rayos agudos
  if (treble > 180) {
    stroke(300, 100, 100, 0.8);
    strokeWeight(2);
    line(width / 2, height / 2, random(width), 0);
  }
}

function mousePressed() {
  if (ready && !sound.isPlaying()) {
    sound.play();
  }
}

function mouseMoved() {
  colorModeValue = map(mouseX, 0, width, 0, 360);
  starDensity = map(mouseY, 0, height, 50, 300);
}

function keyPressed() {
  if (key === 'S') saveCanvas('crusade_visual', 'png');
  if (key === 'W') frameTrigger = 0;
  if (key === 'Z') visualMode = Math.floor(random(4));
}

class Particle {
  constructor(x, y, energy) {
    this.pos = createVector(x + random(-20, 20), y);
    let angle = random(-PI / 3, -2 * PI / 3);
    let speed = map(energy, 0, 255, 2, 12);
    this.vel = p5.Vector.fromAngle(angle).mult(speed);
    this.acc = createVector(0, 0.05);
    this.lifetime = 255;
    this.hue = colorModeValue;
  }

  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.lifetime -= 4;
  }

  show() {
    noStroke();
    fill(this.hue, 100, 100, this.lifetime / 255);
    ellipse(this.pos.x, this.pos.y, 5);
  }

  showGlitch() {
    stroke(this.hue, 100, 100, this.lifetime / 255);
    strokeWeight(random(1, 3));
    point(this.pos.x + random(-2, 2), this.pos.y + random(-2, 2));
  }

  finished() {
    return this.lifetime < 0;
  }
}

``` 
[Link de la simulación](https://editor.p5js.org/tiago123fk/sketches/2K86qyIQl)
### Video
![Resultado del codigo modificado](../../../../assets/VIDEO.mp4)
