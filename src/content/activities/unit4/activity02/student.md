# Conceptos fundamentales
### Primera Simulación: Manejo de ángulos

**¿Qué está pasando en esta simulación? ¿Cuál es la interacción?**  
La simulación muestra cómo se pueden usar rotaciones para modificar la orientación de objetos en la pantalla. A medida que el programa corre, se nota una rotación continua de los elementos gráficos alrededor del centro de la pantalla. No hay interacción directa con el mouse o el teclado, pero el ángulo cambia en cada frame, generando una animación cuando uno presiona alguna tecla.


**¿Por qué se traslada el origen del sistema de coordenadas al centro de la pantalla?**  
Se traslada el origen al centro para que la rotación ocurra alrededor del centro de la pantalla, lo cual da un efecto visual más balanceado. Si no se hiciera, la rotación sucedería alrededor del vértice superior izquierdo (por defecto), lo que puede ser confuso visualmente y difícil de controlar.


**¿Cuál es la relación entre el sistema de coordenadas y la función `rotate()`?**  
La función `rotate()` rota todo el sistema de coordenadas actual. Es decir, después de usar `rotate()`, cualquier figura que se dibuje se verá afectada por esa rotación. Por eso es importante saber en qué punto está el origen antes de rotar.


**¿Por qué se dibuja en (0, 0)? ¿Y por qué los elementos rotan si siempre se dibujan igual?**  
Aunque los elementos se dibujan en la misma posición relativa (por ejemplo, `circle(50, 0, 16)`), están siendo dibujados después de una rotación. Como el sistema de coordenadas fue rotado, las posiciones `(50, 0)` y `(-50, 0)` también están rotadas. Por eso, aunque el código no cambia, los círculos parecen rotar alrededor del centro. Dibujar en `(0, 0)` permite que las rotaciones sean más intuitivas, porque se aplican respecto al centro del objeto.


### Segunda Simulación: Movimiento con dirección
**¿Qué es el marco _motion 101_ en esta simulación?**  
El marco _motion 101_ se refiere al uso de vectores de posición, velocidad y aceleración para simular movimiento. En esta simulación, se usa principalmente la **posición** y la **velocidad** para actualizar la ubicación del objeto y, lo más importante, para orientar su rotación hacia la dirección en la que se mueve.


**¿Qué hace la función `heading()`?**  
La función `heading()` retorna el ángulo (en radianes) del vector de velocidad con respecto al eje x. Es decir, nos da la dirección en la que se está moviendo el objeto. Este ángulo luego se usa para rotar el rectángulo, logrando que el objeto "apunte" hacia donde se está moviendo.


**¿Qué hacen las funciones `push()` y `pop()`?**  
`push()` guarda el estado actual del sistema de coordenadas (posición, rotación, estilos, etc.) y `pop()` lo restaura. Esto permite aplicar transformaciones (como `translate()` o `rotate()`) de forma local sin afectar el resto del dibujo. Es como abrir una "caja temporal" donde modificas cosas, y al cerrarla todo vuelve a la normalidad.


**¿Qué hace `rectMode(CENTER)`?**  
Establece que el rectángulo se dibuja desde su **centro**, no desde la esquina superior izquierda. Esto es útil cuando quieres rotarlo, ya que así el rectángulo gira alrededor de su centro, no de una esquina.


**¿Cuál es la relación entre el ángulo de rotación y el vector de velocidad?**  
El ángulo de rotación que se aplica al objeto es directamente el ángulo del vector de velocidad (usando `.heading()`). Esto asegura que el objeto esté siempre orientado en la dirección en la que se mueve. Si lo dibujas en un papel, verás que el vector velocidad forma un ángulo con el eje x, y esa es la misma rotación que se aplica al objeto usando `rotate(angle)` después de haber trasladado su posición con `translate()`.
