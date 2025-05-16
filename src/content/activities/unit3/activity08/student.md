# Paso por valor y paso por referencia
### Paso por Valor

Se aplica a **tipos de datos primitivos**:


-   Números (`number`)
-   Cadenas de texto (`string`)
-   Booleanos (`boolean`)


Cuando asignamos una variable con un tipo de dato primitivo, se crea una copia independiente. Es decir, cambiar la nueva variable no afecta a la original.


**Ejemplo**
```js
let a = 5;
let b = a;  // Se copia el valor de 'a' en 'b'
b = 10;

console.log(a); // 5  (No cambia)
console.log(b); // 10

```
La variable `b` es una copia independiente de `a`. Modificar `b` no afecta a `a`.

### Paso por Referencia

Se aplica a objetos y estructuras de datos más complejas, como:

-   Vectores (`p5.Vector`)
-   Arreglos (`Array`)
-   Objetos (`Object`)

Cuando asignamos una variable que almacena un objeto, no se crea una copia independiente. En su lugar, ambas variables apuntan a la misma dirección en memoria.


**Ejemplo**
```js
let obj1 = { x: 10 };
let obj2 = obj1; // Ambas variables apuntan al mismo objeto
obj2.x = 20;

console.log(obj1.x); // 20  (Se modifica también en obj1)
console.log(obj2.x); // 20

```
Aquí `obj2` y `obj1` apuntan al mismo objeto en memoria, por lo que cambiar `obj2.x` también cambia `obj1.x`.

### Aplicado al Fragmento de Código
```js
let friction = this.velocity.copy();

```

 - Aquí `friction` es una nueva instancia de `p5.Vector` con los mismos
   valores que `this.velocity`.
 - Modificar `friction` no afectará a `this.velocity` porque es una
   copia independiente.
