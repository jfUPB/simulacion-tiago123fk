# Coordenadas polares
### Primera versión del código (original)
```js
translate(width / 2, height / 2);
let x = r * cos(theta);
let y = r * sin(theta);
line(0, 0, x, y);
circle(x, y, 48);
theta += 0.02;
```
#### ¿Qué está pasando?
Se está utilizando la fórmula de conversión de coordenadas polares a cartesianas: 


X=r * Cos(Theta);   Y=r * Sin(Theta)


-   `r` es la distancia desde el origen.
    
-   `theta` es el ángulo.
    
-   Se dibuja una línea desde el centro hacia ese punto `(x, y)`, que gira con el tiempo porque `theta` va aumentando.
    
-   El resultado es un **movimiento circular**.



### Segunda versión del código
```js
let v = p5.Vector.fromAngle(theta);
line(0, 0, x, y); // <- ¡Error!
circle(v.x, v.y, 48);
```
#### ¿Qué ocurre aquí?

Este código tiene **un error lógico**:

-   Se usa un **vector `v`** creado con un ángulo `theta`, pero no se usa para dibujar la línea.
    
-   Aún intenta dibujar con `x` e `y`, pero esas variables no existen aquí.
    
-   Si se arregla ese error así:

```js
let v = p5.Vector.fromAngle(theta);
line(0, 0, v.x, v.y);
circle(v.x, v.y, 48);
```
#### ¿Qué pasa entonces?

-   El vector `v` tiene módulo 1 por defecto (longitud).
    
-   Entonces el círculo se dibuja muy cerca del centro, girando sobre una circunferencia de radio 1 (casi invisible).
    
-   Se mueve correctamente, pero apenas se nota porque el radio es muy pequeño.


#### Tercera versión del código
```js
let v = p5.Vector.fromAngle(theta, r);
line(0, 0, v.x, v.y);
circle(v.x, v.y, 48);
```
#### ¿Qué ocurre aquí?

-   Ahora sí se crea un vector polar correctamente con **ángulo `theta` y módulo `r`**.
    
-   El vector `v` se convierte automáticamente a coordenadas cartesianas.
    
-   El círculo gira a una **distancia fija `r` del centro**.
    
-   Es lo mismo que la fórmula, pero usando un **objeto vectorial** que lo hace todo.
