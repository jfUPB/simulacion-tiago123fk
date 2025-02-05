# Diseño: exploración de la idea
### **Intención de Diseño**

Mi intención es crear una aplicación interactiva en tiempo real que genere una pieza de **arte generativo algorítmico**, combinando diferentes conceptos explorados en las actividades anteriores. La idea es desarrollar un sistema visual que **reaccione a la música o a la entrada del micrófono**, generando patrones dinámicos que evolucionen en el tiempo. Esta aplicación permitirá a los usuarios interactuar con los elementos gráficos, modificando su comportamiento en tiempo real mediante la entrada de audio y el movimiento del mouse.
### **Conceptos Utilizados y Justificación**

1.  **Ruido Perlin (Para movimientos suaves y naturales)**
    
    -   Usaré el **ruido Perlin** para generar desplazamientos fluidos en los elementos visuales, evitando movimientos abruptos y creando una estética más orgánica. Esto servirá para simular el comportamiento de partículas o elementos gráficos que fluyen de manera natural con la música.
2.  **Lévy Flight (Para variaciones dinámicas en los efectos visuales)**
    
    -   Implementaré un patrón de **Lévy Flight** en la distribución de ciertos elementos visuales. Esto permitirá que la mayoría de los movimientos sean sutiles, pero ocasionalmente ocurran **saltos inesperados** en la composición, generando momentos de mayor intensidad visual en respuesta a cambios en la música.
3.  **Distribución Normal (Para variaciones en el tamaño de las partículas y su comportamiento visual)**
	- Se aplicará una **distribución normal** para definir los **tamaños de las partículas**, asegurando que la mayoría tenga un tamaño medio y solo algunas sean significativamente más grandes o más pequeñas.
 4. **Arte generativo con interacción en tiempo real (Audio/Micrófono)**
    
    -   La aplicación reaccionará en **tiempo real** al sonido capturado por el micrófono, modificando parámetros como el color, la velocidad de los elementos y la intensidad del movimiento. También se podrá interactuar con el mouse para alterar la estructura de los patrones generados.


### **Referentes e Inspiración**

Para este diseño me inspiré en varios artistas y proyectos de **arte generativo y visualización de audio**, como:

-   **Refik Anadol**: Su uso de datos en movimiento y efectos visuales inspirados en la música.
-   **Casey Reas**: Su trabajo en Processing y exploración de patrones visuales generativos.
-   **Patrik Hübner**: Aplicaciones de diseño generativo que responden a estímulos en tiempo real.
