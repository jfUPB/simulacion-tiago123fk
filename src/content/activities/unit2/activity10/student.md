# Diseño: exploración de la idea
### Intención de Diseño

El objetivo de esta aplicación es crear una visualización de arte generativo interactivo donde las partículas respondan a la música en tiempo real.


**Interacción con la música:**


-   Las partículas cambian de tamaño, velocidad y color en función de la intensidad del sonido.
-   Las frecuencias bajas afectan el tamaño, las medias la velocidad, y las altas el color.
-   Se agregan partículas progresivamente y se eliminan para optimizar el rendimiento.


**Interacción con el usuario:**


-   El usuario puede mover el mouse para influir en las partículas.
-   Al hacer clic, la canción se reproduce o se pausa.


Este diseño fusiona sonido y visualización interactiva, permitiendo que la música se convierta en una forma de arte generativo en tiempo real.


### Aplicación del Marco Motion 101

La aplicación sigue el modelo de **Motion 101**, que establece que la aceleración controla la velocidad y la velocidad controla la posición.


**Cada partícula tiene tres propiedades fundamentales:**


-   **Posición (`position`)**  Dónde se encuentra en la pantalla.
-   **Velocidad (`velocity`)** En qué dirección y qué tan rápido se mueve.
-   **Aceleración (`acceleration`)**  Qué fuerzas externas afectan su movimiento.


**Cómo la música afectara el movimiento:**


-   **Frecuencias bajas (`bass`)**  Modifican el tamaño de la partícula.
-   **Frecuencias medias (`mid`)**  Afectan la velocidad.
-   **Frecuencias altas (`treble`)**  Cambian el color.


aplicamos Motion 101 para que la aceleración (frecuencia del sonido) cambie la velocidad y la posición de las partículas en la pantalla.

### **Referentes Utilizados**


 **Inspiraciones principales:**


-   **Daniel Shiffman (The Nature of Code):** Simulación de partículas y Motion 101.
-   **Visualizadores de música como Winamp y MilkDrop:** Transformar audio en arte generativo.
-   **Refik Anadol:** Uso de datos y sonido para generar arte visual interactivo.
