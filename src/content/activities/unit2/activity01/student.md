# Analiza una aplicación interactiva
- ###  ¿Cómo funciona la suma de dos vectores?
La suma de vectores se basa en el principio de componente a componente, lo que significa que se suman las coordenadas correspondientes de cada vector.


En el contexto de **p5.js**, cuando tenemos un vector de **posición** y un vector de **velocidad**, la suma de estos permite actualizar la posición del objeto en cada frame del programa.


En código de p5.js:
```js
position.add(velocity);
```
En este caso, el vector `position` se actualiza sumándole el vector `velocity`, lo que hace que el objeto se mueva de forma continua en la dirección establecida.

- ### ¿Por qué esta línea `position = position + velocity;` no funciona?
no funciona en p5.js porque los vectores no pueden sumarse directamente como números. En JavaScript, `position` y `velocity` son objetos de tipo `p5.Vector`, por lo que no se pueden operar con `+` de manera directa.


 **Error:**  
Cuando intentamos `position + velocity`, JavaScript intenta concatenar los objetos en una cadena de texto en lugar de sumarlos matemáticamente.


 **Solución correcta:**  
En lugar de usar `+`, debemos utilizar el método `.add()` de los objetos `p5.Vector`:
