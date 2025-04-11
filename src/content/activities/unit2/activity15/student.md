# Autoevaluación
### Evaluación de mi nivel de comprensión
**Mi autoevaluación: 4/5**

-   Considero que tengo un muy buen dominio de los conceptos de la unidad, pero aún hay áreas en las que puedo mejorar y profundizar.

### Justificación y ejemplos concretos de mi trabajo

**Comprensión y aplicación de Motion 101** (**Nivel: 4/5**)

-   **Ejemplo en mi trabajo:** Implementé correctamente posición, velocidad y aceleración en las partículas de la simulación.
```js
this.velocity.add(this.acceleration); // La aceleración cambia la velocidad
this.position.add(this.velocity); // La velocidad cambia la posición
this.acceleration.mult(0); // Se reinicia la aceleración
```

**Implementación de vectores en simulación de movimiento** (**Nivel: 4.5/5**)

-   **Ejemplo en mi trabajo:** Usé correctamente `p5.Vector` para controlar la dirección y velocidad de las partículas.

```js
let force = p5.Vector.random2D().mult(bass / 100); // Movimiento según bajos
p.applyForce(force);
```

### Áreas donde necesito reforzar mi aprendizaje
- Explorar más variaciones de Motion 101, como aplicaciones de fuerzas externas más complejas como viento o gravedad personalizada.
- En este proyecto usé mouse y audio, pero en el futuro me gustaría experimentar con entrada de cámara (webcam) o sensores de dispositivos móviles para crear una experiencia aún más interactiva.
- Mejorar la optimización de simulaciones con muchas partículas
