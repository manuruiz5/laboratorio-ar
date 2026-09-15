# Búsqueda del Tesoro AR — Sacré Coeur

El juego tiene tres marcadores. Los dos primeros son los que ya vienen con AR.js (Hiro y Kanji), y el tercero es uno que generamos con la herramienta de patrones de AR.js para que fuera especial, como el "escondite final". Cada marcador, al ser detectado por la cámara, hace aparecer un objeto 3D armado en A-Frame flotando junto con el texto de la pista correspondiente. Arriba de la pantalla hay una barra de progreso que se va completando a medida que se encuentran las pistas, y cuando el jugador ya escaneó las tres aparece una pantalla final dorada con un mensaje de "tesoro encontrado".

Una cosa que nos pareció importante resolver fue que el progreso no se pierda si alguien recarga la página a mitad de la búsqueda: por eso el estado se guarda en el `localStorage` del celular, y una pista ya encontrada queda marcada aunque el marcador se pierda de la cámara. Todo el juego vive en un solo archivo, `index.html`.

## Cómo probarlo

El juego está publicado acá:

**https://manuruiz5.github.io/laboratorio-ar/**

Hay que abrirlo desde el celular o computadora (Chrome en Android o Safari en iOS) y aceptar el permiso de cámara. Para jugarlo hacen falta los tres marcadores impresos o mostrados en otra pantalla:

- **Marcador 1 (Hiro):** https://raw.githubusercontent.com/AR-js-org/AR.js/master/data/images/hiro.png
- **Marcador 2 (Kanji):** https://raw.githubusercontent.com/AR-js-org/AR.js/master/three.js/examples/marker-training/examples/pattern-images/pattern-kanji.png
- **Marcador 3 (personalizado):** la imagen que está en `patterns/custom-marker.png`

Un consejo: mejor que estén bien iluminados y no muy chiquitos, porque si están arrugados o con poca luz la cámara tarda en engancharlos. Apuntando el celular a cada uno debería aparecer el objeto 3D con la pista, y al pasar por los tres se desbloquea la pantalla final.
