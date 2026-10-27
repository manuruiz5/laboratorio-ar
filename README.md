# Búsqueda del Tesoro AR — Sacré Coeur

El juego tiene tres marcadores. Los dos primeros son los que ya vienen con AR.js (Hiro y Kanji), y el tercero, "la llave", es un marcador de tipo barcode (código 3x3 número 5), que AR.js reconoce sin necesitar un archivo de patrón y marca el "escondite final". Cada marcador, al ser detectado por la cámara, hace aparecer un objeto 3D armado en A-Frame flotando junto con el texto de la pista correspondiente. Arriba de la pantalla hay una barra de progreso que se va completando a medida que se encuentran las pistas, y cuando el jugador ya escaneó las tres aparece una pantalla final dorada con un mensaje de "tesoro encontrado".

Una cosa que nos pareció importante resolver fue que el progreso no se pierda si alguien recarga la página a mitad de la búsqueda: por eso el estado se guarda en el `localStorage` del celular, y una pista ya encontrada queda marcada aunque el marcador se pierda de la cámara. Todo el juego vive en un solo archivo, `index.html`.

## Cómo probarlo

El juego está publicado acá:

**https://manuruiz5.github.io/laboratorio-ar/**

Hay que abrirlo desde el celular o computadora (Chrome en Android o Safari en iOS) y aceptar el permiso de cámara. Al entrar aparece un cartel de "Cómo jugar" que explica el juego y tiene un botón para ver los marcadores.

Los tres marcadores están juntos en una página aparte, `marcadores.html`, pensada para abrirla en otra pantalla (compu o tablet) y escanearlos desde el celular:

**https://manuruiz5.github.io/laboratorio-ar/marcadores.html**

Las imágenes están guardadas en el proyecto, en la carpeta `markers/`, así no dependen de links externos:

- **Marcador 1 (Hiro):** `markers/hiro.png`
- **Marcador 2 (Kanji):** `markers/kanji.png`
- **Marcador 3 (la llave):** `markers/llave.png`, barcode 3x3 con el valor 5. La escena usa `detectionMode: mono_and_matrix` y `matrixCodeType: 3x3` para que conviva con Hiro y Kanji.

Un consejo: mejor que estén bien iluminados y no muy chiquitos, porque si están arrugados o con poca luz la cámara tarda en engancharlos. Apuntando el celular a cada uno debería aparecer el objeto 3D con la pista, y al pasar por los tres se desbloquea la pantalla final.
