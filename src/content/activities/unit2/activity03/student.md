# Experimenta

-   ### ¿Qué resultado esperas obtener?


En este experimento, tenemos un vector `posicion` que inicialmente tiene los valores `(6,9)`. Luego, lo pasamos a la función `playingVector(v)`, donde cambiamos sus valores a `(20,30)`.


Como `p5.Vector` es un objeto, lo que espero que pase es que cuando imprimamos `posicion` después de llamar `playingVector(posicion)`, veremos que sus valores realmente cambiaron a (20,30) porque la función modificó el objeto original.



- ###   ¿Qué resultado obtuviste?

Cuando probé el código, lo que pasó fue que la posición del vector realmente cambió después de que llamamos la función `playingVector(posicion)`.

Primero, `posicion` empieza con los valores `(6,9)`, pero en la función `playingVector(v)`, le asignamos `v.x = 20;` y `v.y = 30;`. Como `p5.Vector` es un objeto, no estamos creando una copia, sino que estamos modificando directamente la misma referencia en la memoria.


- ### Recuerda los conceptos
	### Paso por valor:


En JavaScript, los **tipos primitivos** (números, booleanos, strings) se pasan **por 		valor**, lo que significa que se copia el contenido y cualquier cambio dentro de una función **no afecta la variable original**.


**Ejemplo**
```js
function cambiarValor(num) {
  num = 10;
}

let a = 5;
cambiarValor(a);
console.log(a);  // Sigue siendo 5

```
Aquí, `num` es una **copia de `a`**, por lo que `a` no cambia.


### Paso por Referencia:

Los **objetos y arreglos**, incluyendo `p5.Vector`, se pasan **por referencia**, lo que significa que cualquier cambio dentro de una función **afecta la variable original**.


**Ejemplo**
```js
function cambiarObjeto(obj) {
  obj.valor = 10;
}

let objeto = { valor: 5 };
cambiarObjeto(objeto);
console.log(objeto.valor);  // Ahora es 10

```
Aquí, `objeto` es una **referencia**, por lo que `cambiarObjeto()` modifica directamente su contenido.


- ###   ¿Qué tipo de paso se está realizando en el código?

En este código, se está usando **paso por referencia** porque `p5.Vector` es un objeto. Esto significa que cuando pasamos `posicion` a la función `playingVector(v)`, no se crea una copia nueva, sino que estamos trabajando directamente con el mismo vector en memoria. Por eso, cualquier cambio que hagamos dentro de la función afecta la variable original fuera de ella.

- ### ¿Qué aprendiste?
	- Los vectores en p5.js se pasan por referencia lo que significa que cualquier modificación dentro de una función cambiará la variable original.  
	- En JavaScript, los tipos primitivos (números, strings, booleanos) se pasan por valor, mientras que los objetos y arreglos se pasan por referencia.  
	- Es importante tener esto en cuenta al manipular vectores en simulaciones, ya que los cambios en una función afectarán el objeto original.
