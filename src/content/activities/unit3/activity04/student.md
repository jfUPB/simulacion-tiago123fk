# Marco Motion 101
### 1. ¿Dónde está el marco Motion 101 en el código?

El marco Motion 101 se basa en los tres conceptos fundamentales del movimiento en programación:

1.  **Posición**  `this.position.add(this.velocity);`
2.  **Velocidad**  `this.velocity.add(this.acceleration);`
3.  **Aceleración**  `this.acceleration` (se calculará en esta unidad)

En el código proporcionado, el marco Motion 101 está en la función `update()`, donde la posición del objeto se actualiza sumándole la velocidad, y la velocidad se actualiza sumándole la aceleración.

```js
update() { // Aquí calculo la aceleración 
.
. 
. 
this.velocity.add(this.acceleration); // Actualiza la velocidad con la aceleración
this.velocity.limit(this.topSpeed); // Limita la velocidad
this.position.add(this.velocity); // Actualiza la posición con la velocidad
```

Este marco establece que cualquier objeto en movimiento debe actualizar su posición en función de su velocidad, y su velocidad en función de su aceleración.

### 2. ¿Cuáles eran los algoritmos para definir la aceleración en la unidad anterior?

En la unidad anterior, la aceleración no se calculaba con fuerzas, sino que se definía a partir de reglas algorítmicas o manipulaciones directas. Aquí hay algunos ejemplos:

#### Ejemplo 1: Aceleración aleatoria

En este caso, la aceleración se asigna con un valor aleatorio en cada fotograma.
```js
update() {
    this.acceleration = createVector(random(-0.01, 0.01), random(-0.01, 0.01));
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topSpeed);
    this.position.add(this.velocity);
}
```
**Explicación**: Se genera un vector de aceleración aleatorio en cada frame, lo que da un movimiento errático.


#### Ejemplo 2: Aceleración hacia el mouse

Aquí, la aceleración se calcula en función de la dirección hacia el puntero del mouse.

```js
update() {
    let mouse = createVector(mouseX, mouseY);
    this.acceleration = p5.Vector.sub(mouse, this.position);
    this.acceleration.setMag(0.05);  // Ajusta la magnitud de la aceleración
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topSpeed);
    this.position.add(this.velocity);
}

```


### 3. ¿Cómo cambia la forma de definir la aceleración en esta unidad?

En esta unidad, en lugar de asignar directamente un valor a la aceleración, ahora la calculamos con base en fuerzas externas, aplicando la Segunda Ley de Newton


`Fuerza = Masa * Aceleración`

Esto significa que la aceleración ya no es arbitraria, sino que depende de la fuerza aplicada y de la masa del objeto.

#### Ejemplo: Calculando la aceleración con una fuerza aplicada
```js
applyForce(force) {
    let f = p5.Vector.div(force, this.mass); // a = F / m
    this.acceleration.add(f);
}

update() {
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.topSpeed);
    this.position.add(this.velocity);
    
    // Se reinicia la aceleración para el siguiente ciclo
    this.acceleration.mult(0);
}

```

**Explicación**:

-   Ahora la aceleración depende de una fuerza aplicada, que se divide por la masa del objeto.
-   Se usa `applyForce(force)` para aplicar fuerzas externas.
-   Después de actualizar la posición, la aceleración se reinicia (`mult(0)`) para que no se acumule.

### 4. Relación con las Leyes de Newton

La principal conexión con las Leyes de Movimiento de Newton es la **Segunda Ley**:


 `Fuerza = Masa * Aceleración`


Esta ley nos dice que la aceleración no es arbitraria, sino que surge de una fuerza aplicada y depende de la masa del objeto.


-   En la unidad anterior, se asignaba la aceleración manualmente, sin relación con fuerzas.
-   En esta unidad, la aceleración se calcula a partir de fuerzas externas, lo que permite una simulación más realista del movimiento.


También podemos conectar con la **Primera Ley de Newton** (Inercia):

-   Si no hay ninguna fuerza actuando (`F = 0`), entonces la aceleración es `0` y el objeto mantiene su velocidad constante.


Y con la **Tercera Ley de Newton** (Acción-Reacción):

-   Si el objeto choca contra un borde (`checkEdges()`), el código puede aplicar una **fuerza de reacción** para cambiar su dirección.
