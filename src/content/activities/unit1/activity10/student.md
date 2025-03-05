# Análisis de resultados

### **Desafíos Encontrados**

 **Integrar múltiples conceptos sin perder coherencia**

-   Uno de los mayores retos fue combinar de manera efectiva **Ruido Perlin, Lévy Flight, Distribución Normal y Arte Generativo** en una misma aplicación.
-   Al principio, algunos elementos parecían competir entre sí en lugar de complementarse, lo que requería ajustes en los parámetros para lograr una fluidez visual y una composición equilibrada.

 **Controlar la aleatoriedad para evitar resultados caóticos**

-   Aunque la aleatoriedad es el núcleo del arte generativo, en algunos momentos los patrones generados parecían demasiado caóticos o desorganizados.
-   Fue clave encontrar un balance entre variabilidad y estructura, ajustando la **frecuencia de los saltos Lévy**, la **escala del ruido Perlin** y la **distribución de tamaños y velocidades** mediante la Distribución Normal.

 **Interacción con el usuario y respuesta al sonido**

-   Incorporar la interacción con el **mouse y el micrófono** presentó el desafío de **sincronizar los cambios visuales con la entrada de audio** de manera efectiva.
-   En versiones iniciales, la respuesta al sonido era demasiado brusca o sutil, por lo que hubo que **ajustar el mapeo de valores** y la sensibilidad para lograr una interacción fluida.


### **Lecciones Aprendidas**

 **La combinación de diferentes tipos de aleatoriedad puede generar patrones más interesantes y realistas**

-   Usar **Ruido Perlin** para movimientos suaves, **Lévy Flight** para variaciones impredecibles y **Distribución Normal** para controlar tamaños y velocidades ayudó a crear una simulación más natural.

 **La aleatoriedad necesita control y dirección para ser efectiva**

-   Aunque la aleatoriedad genera diversidad en la composición, es importante **definir límites y reglas** para que el resultado final sea coherente y visualmente atractivo.


**Es importante ajustar parámetros y experimentar con valores hasta encontrar un balance**

-   Muchas veces, pequeños cambios en los valores de ruido, probabilidades o sensibilidad al audio pueden mejorar significativamente la experiencia visual.


### Conclusión
Hacer esta aplicación fue un proceso de prueba y error, donde me di cuenta de que la aleatoriedad, aunque suene como algo desordenado, necesita cierto control para que los resultados sean visualmente atractivos y coherentes. Uno de los mayores aprendizajes fue encontrar ese equilibrio entre el caos y la estructura, combinando diferentes tipos de aleatoriedad para lograr algo dinámico pero sin que se viera demasiado caótico.

También aprendí que la interacción hace que todo se sienta más vivo. Poder modificar la visualización con el sonido y el mouse le da otro nivel de profundidad a la experiencia, haciendo que no solo sea arte generativo, sino algo con lo que realmente puedes jugar.

Al final, este proyecto me hizo ver que el arte generativo es un camino de exploración sin un único resultado correcto. Siempre hay maneras de ajustar los parámetros y probar cosas nuevas para mejorar la experiencia. Y lo mejor de todo es que siempre se puede seguir experimentando y descubriendo nuevas formas de jugar con la aleatoriedad.
