# 🏰 Búsqueda del Tesoro AR — Edificio Sacré Coeur

Juego de realidad aumentada basado en marcadores (AR.js + A-Frame). El jugador
escanea 3 marcadores físicos distribuidos en el edificio; cada uno revela una
pista en 3D. Al escanear los tres, se desbloquea la pantalla final de "tesoro
encontrado" (con sonido).

## Estructura del proyecto

```
laboratorio-ar/
├── index.html          → toda la lógica del juego (A-Frame + AR.js + JS)
├── patterns/
│   ├── README.md        → instrucciones para generar el 3er marcador
│   └── custom-marker.patt   
└── README.md            → este archivo
```

## Cómo funciona el juego

- **Marcador 1 — Hiro** (preset incluido en AR.js): muestra la Pista 1.
- **Marcador 2 — Kanji** (preset incluido en AR.js): muestra la Pista 2.
- **Marcador 3 — patrón personalizado**: muestra la Pista 3 / tesoro final.
- Un HUD arriba de la pantalla muestra cuántas pistas (0 a 3) ya se
  encontraron, con un mensaje corto ("toast") cada vez que se detecta un
  marcador nuevo, más un sonido (`markerFound`).
- Una vez encontrado, un marcador "cuenta" para siempre aunque se pierda de
  cámara (`markerLost` no resetea el progreso).
- El progreso se guarda en `localStorage` del celular, así que si alguien
  recarga la página a mitad de la búsqueda no pierde lo ya encontrado.
- Al juntar las 3 pistas aparece la pantalla final con un mensaje, animación y
  una pequeña fanfarria generada con Web Audio API (no requiere archivos de
  audio externos).

---

## 1. Probarlo en tu computadora (localhost)

Los navegadores solo permiten usar la cámara en un **contexto seguro**:
`https://` o `http://localhost`. Por eso no alcanza con abrir el `index.html`
haciendo doble clic (`file://`) — hay que servirlo con un servidor local.

Desde esta carpeta, elegí una opción (con tener Python 3 alcanza en casi
cualquier Mac):

```bash
cd "/Users/manuelaruiz/Desktop/tecnología para negocios digitales/laboratorio-ar"
python3 -m http.server 8080
```

Luego abrí en el navegador de tu computadora:

```
http://localhost:8080
```

Aceptá el permiso de cámara. Imprimí o mostrá en otra pantalla/celular la
imagen del marcador Hiro (ver paso 3) y apuntá la cámara de la compu hacia
ella — debería aparecer el cofre 3D con la Pista 1.

> Alternativas equivalentes si no tenés Python: `npx serve` (Node.js) o la
> extensión "Live Server" de VS Code. Cualquiera sirve, lo importante es que
> quede accesible por `http://localhost:PUERTO`.

### ⚠️ Probarlo en el celular *antes* de publicar

Un celular normalmente no puede acceder a `http://localhost:8080` de tu
computadora, y Chrome/Safari en Android/iOS **exigen HTTPS** para usar la
cámara (salvo que sea el propio localhost del celular). Como el proyecto es
estático, el camino más simple es:

- Directamente publicarlo en GitHub Pages (paso 2) — te da HTTPS gratis en un
  minuto y podés iterar hostpackage rápido, o
- Si querés probarlo en el celular sin publicar todavía, usar un túnel HTTPS
  temporal como [ngrok](https://ngrok.com/) (`ngrok http 8080`) apuntando a tu
  servidor local.

Para este laboratorio, lo más simple y directo es probar la lógica del juego
en la compu con el marcador en pantalla, y usar GitHub Pages como el entorno
real de prueba en el celular.

---

## 2. Publicarlo en GitHub Pages

1. Creá un repositorio nuevo en GitHub (público), por ejemplo
   `busqueda-tesoro-ar`.
2. Desde esta carpeta, inicializá git y subí el proyecto:

   ```bash
   cd "/Users/manuelaruiz/Desktop/tecnología para negocios digitales/laboratorio-ar"
   git init
   git add index.html README.md patterns
   git commit -m "Búsqueda del tesoro AR - Sacré Coeur"
   git branch -M main
   git remote add origin https://github.com/TU-USUARIO/busqueda-tesoro-ar.git
   git push -u origin main
   ```

3. En GitHub, andá a **Settings → Pages**.
4. En "Build and deployment" → "Source", elegí **Deploy from a branch**.
5. En "Branch" elegí `main` y la carpeta `/ (root)`, y guardá.
6. Esperá 1-2 minutos. GitHub te va a dar una URL del estilo:

   ```
   https://TU-USUARIO.github.io/busqueda-tesoro-ar/
   ```

7. Abrí esa URL desde el celular (con datos móviles o wifi), aceptá el
   permiso de cámara, y probá escaneando los marcadores impresos.

Esa URL es el entregable final que le vas a pasar a Bruno, Maxi y Gonzalo.

> Cada vez que hagas cambios en `index.html`, repetí `git add`, `git commit` y
> `git push` — GitHub Pages se actualiza solo, en general en menos de un
> minuto.

---

## 3. Conseguir e imprimir los 3 marcadores

Los tres marcadores deben imprimirse en tamaño real (al menos 15x15 cm
recomendado, más grande si el punto de escaneo está a más de 1 metro) sobre
fondo blanco, sin plastificar con brillo (el reflejo dificulta la detección),
y bien iluminados en el lugar donde se coloquen.

### Marcador 1 — Hiro

Es el marcador clásico de AR.js/ARToolKit (ya "sabe" reconocerlo la librería,
no hace falta generar nada). Descargalo de:

- https://raw.githubusercontent.com/AR-js-org/AR.js/master/data/images/hiro.png

Imprimilo tal cual, sin recortar el margen blanco alrededor del cuadrado
negro (ese margen es necesario para que la cámara lo detecte bien).

### Marcador 2 — Kanji

También viene incluido en AR.js. Descargalo de:

- https://raw.githubusercontent.com/AR-js-org/AR.js/master/three.js/examples/marker-training/examples/pattern-images/pattern-kanji.png

Mismo criterio de impresión: dejar el borde blanco, sin brillo.

### Marcador 3 — Marcador personalizado (Pista 3 / tesoro)

Este lo generás vos con la herramienta oficial de AR.js, así podés usar un
dibujo propio (por ejemplo un cofre, una calavera, el logo del Sacré Coeur,
etc.):

1. Entrá a la herramienta oficial:
   https://ar-js-org.github.io/AR.js/three.js/examples/marker-training/examples/generator.html
2. Subí una imagen cuadrada, con **buen contraste y sin simetría** (evitá
   círculos perfectos o figuras que se vean igual rotadas 90°/180°, porque
   confunden a la cámara sobre la orientación). Un dibujo simple en blanco y
   negro funciona mejor que una foto con detalle fino.
3. Descargá:
   - El archivo **`.patt`** (botón "Download Marker") → renombralo a
     `custom-marker.patt` y colocalo dentro de la carpeta `patterns/` de este
     proyecto (reemplazando el que ya está ahí).
   - La **imagen/PDF del marcador** ("Download Image" o alguna opción
     "PDF...per Page") → **esta es la que se imprime**, no el `.patt` (el
     `.patt` es solo el archivo que usa el código para reconocer el dibujo).
4. Subí el `custom-marker.patt` actualizado al repositorio (`git add`,
   `git commit`, `git push`) para que quede publicado en GitHub Pages junto
   con el resto del proyecto.

> Si no generás tu propio marcador, el juego igual funciona con las pistas 1 y
> 2 (Hiro y Kanji), pero la pista 3 no se va a activar hasta que exista
> `patterns/custom-marker.patt`. Ver `patterns/README.md` para más detalle.

### Dónde colocar los marcadores físicamente

Pegá cada marcador impreso en un punto distinto del Edificio Sacré Coeur
(por ejemplo: entrada, algún pasillo o cartelera, y un aula o patio),
asegurándote de que:

- Haya buena luz (evitar contraluz fuerte o sombras sobre el marcador).
- El marcador quede plano (no arrugado ni doblado) y a una altura cómoda para
  apuntar con el celular.
- Haya espacio para que el jugador se pare a 40 cm - 1,5 m de distancia y
  apunte de frente.

---

## 4. Cómo lo van a jugar Bruno, Maxi y Gonzalo

1. Abren la URL de GitHub Pages desde el navegador del celular (Chrome en
   Android o Safari en iOS).
2. Aceptan el permiso de cámara.
3. Recorren el edificio apuntando la cámara a cada marcador impreso.
4. Cada marcador encontrado suma al contador de arriba de la pantalla y
   dispara un sonido corto.
5. Al encontrar los 3, aparece la pantalla dorada de "TESORO ENCONTRADO" con
   la fanfarria final.

Si alguno cierra la app o recarga la página a mitad de camino, el progreso
queda guardado en ese celular (no hace falta volver a escanear lo ya
encontrado).

---

## Personalizar textos, colores o modelos 3D

Todo el contenido de cada pista está en `index.html`, dentro de cada
`<a-marker>`. Se puede:

- Cambiar el texto de `<a-text value="...">` (usar `\n` para salto de línea).
- Cambiar la forma (`a-box`, `a-sphere`, `a-cone`) por otras primitivas de
  A-Frame (`a-cylinder`, `a-torus`, `a-plane`, etc.) o por un modelo 3D
  (`a-entity gltf-model="url(...)"`) si se agrega uno a `a-assets`.
- Cambiar colores con el atributo `color`.
- Editar los mensajes del HUD/toast en la sección `<script>` al final del
  archivo (objeto `clueMessages`).
