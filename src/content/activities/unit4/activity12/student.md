# Consolidación
### ¿Qué concepto de oscilación utilizaste como base para tu obra? Describe cómo lo implementaste.

Utilicé el concepto de **movimiento oscilatorio sinusoidal**, específicamente la función `sin()` para generar ondas que se repiten suavemente a lo largo del tiempo. Cada elemento visual (círculo, línea o triángulo) en la obra se mueve verticalmente como si siguiera una onda. Además, el volumen del micrófono controla la **amplitud de esa oscilación**, lo que da como resultado un movimiento más intenso cuando el sonido es más fuerte, y más sutil cuando hay silencio.

### ¿Cómo funciona la interacción en tu obra? Explica cómo el usuario puede modificar la obra en tiempo real.

La obra es interactiva en tiempo real a través de dos mecanismos:

1.  **Entrada por micrófono:** el volumen del sonido afecta directamente el tamaño, posición y color de los elementos visuales. Hablar más fuerte genera movimientos más amplios y colores más intensos.
    
2.  **Teclado:** el usuario puede cambiar entre tres modos visuales (círculos, líneas y triángulos) presionando las teclas `1`, `2` o `3`, lo que permite explorar diferentes estilos dentro de la misma obra.


### ¿Qué desafíos encontraste durante el proceso de creación? ¿Cómo los superaste?

Uno de los desafíos fue lograr que la interacción con el micrófono se sintiera natural y fluida, sin que la visualización reaccionara de forma exagerada o errática. Al inicio, el volumen se acumulaba y la visualización se volvía muy rápida o incontrolable. Para solucionarlo, ajusté los rangos con `map()` y agregué efectos como suavizado visual (estela) y una constante de oscilación para mantener la fluidez aunque a veces no me cuadraba.  


También fue un reto lograr una obra que se sintiera estéticamente atractiva sin sobrecargarla; para eso probé varias paletas de color y estilos hasta encontrar un equilibrio.

### ¿Qué aprendiste sobre las oscilaciones y su aplicación en el arte generativo?

Aprendí que las oscilaciones no solo son un fenómeno físico, sino que pueden ser una herramienta poderosa para crear movimiento y vida en el arte generativo. Usar funciones como `sin()` o `cos()` permite simular comportamientos naturales como olas, respiración o pulsos. También descubrí cómo combinar estas funciones con datos en tiempo real (como el micrófono) para crear obras reactivas e inmersivas, que responden directamente a la presencia del usuario. Esta conexión entre **física, código y expresión visual** me parece muy potente y abre muchas posibilidades para futuras creaciones.

### Conclusión: Visuales generativos para eventos de DJ

Después de explorar oscilaciones, ondas, fuerzas y su interacción con entradas como el micrófono, entendí que puedo utilizar estos conceptos para crear visuales generativos en vivo que reaccionen al sonido en tiempo real. Usando herramientas como p5.js y funciones como `sin()`, `map()`, y `getLevel()`, puedo construir sistemas visuales que se sincronicen con la música, cambiando color, forma y movimiento según la energía del ambiente.


Este enfoque no solo es visualmente llamativo, sino que también permite una conexión directa entre lo que suena y lo que se ve, logrando una experiencia inmersiva para el público. En un evento de DJ, estas visuales pueden proyectarse en pantallas, responder al beat, al volumen o incluso a frecuencias específicas con FFT, transformando el espacio en una obra interactiva en constante evolución.


Todo lo aprendido me da la base para seguir experimentando, escalar esta obra y desarrollar herramientas visuales que acompañen sets de música electrónica, live coding o performances audiovisuales.
