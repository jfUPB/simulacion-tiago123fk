# Explora posibilidades

 - ### ¿Para qué sirve el método mag()?
El método `mag()` devuelve la **magnitud (longitud)** de un vector, es decir, qué tan grande es su tamaño en el espacio.
- ### ¿Cuál es la diferencia entre mag() y magSq()? ¿Cuál es más eficiente?
	-   `mag()` calcula la raíz cuadrada de la suma de los cuadrados de los componentes, devolviendo la longitud real del vector.
	-   `magSq()` devuelve la misma suma pero sin sacar la raíz cuadrada, es decir, el cuadrado de la magnitud.


`magSq()` es más eficiente porque evita el cálculo de la raíz cuadrada, que es más costoso computacionalmente. Se usa cuando solo necesitas comparar magnitudes y no la longitud exacta.


- ### ¿Para qué sirve el método normalize()?
`normalize()` convierte un vector en **un vector unitario**, es decir, mantiene su dirección pero cambia su magnitud a 1.


- ### ¿Cómo explicarle a un periodista qué hace el método dot() en una sola frase?


El método `dot()` calcula el producto punto, que mide qué tanto dos vectores apuntan en la misma dirección. Si el resultado es positivo, van en una dirección similar, si es cero, son perpendiculares, si es negativo, van en direcciones opuestas.


- ### Diferencia entre la versión estática y de instancia de dot()
	- **Versión de instancia:** Se usa en un objeto vector y se le pasa otro vector.
	- **Versión estática:** Se usa directamente desde `p5.Vector.dot(v1, v2)`, sin necesidad de un objeto.


	- **Ambas hacen lo mismo**, pero la estática es útil cuando trabajamos con vectores que no queremos modificar directamente.


- ### ¿Cuál es la interpretación geométrica del producto cruz?
El producto cruz de dos vectores genera otro vector perpendicular a los dos originales.

 
 La **magnitud** del resultado representa el área del paralelogramo formado por los dos vectores.


  La **orientación** sigue la regla de la mano derecha: Si usas la mano derecha y alineas los dedos con el primer vector y los cierras hacia el segundo, el pulgar apunta en la dirección del producto cruz.


- ### ¿Para qué sirve el método dist()?


`dist()` calcula la **distancia entre dos puntos** en el espacio.


- ### ¿Para qué sirven los métodos normalize() y limit()?


**normalize()**


  Convierte un vector en un **vector unitario**, lo que permite trabajar solo con direcciones sin importar la magnitud.


 **limit()**


 Restringe la magnitud de un vector a un valor máximo. Es útil para evitar que un objeto se mueva demasiado rápido.


