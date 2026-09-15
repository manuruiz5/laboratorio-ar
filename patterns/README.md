# Carpeta de patrones personalizados

`index.html` espera encontrar acá el archivo:

```
patterns/custom-marker.patt
```

Ese archivo **todavía no existe** — hay que generarlo una sola vez siguiendo el
paso "3. Generar el marcador personalizado (Pista 3)" del `README.md` principal
del proyecto.

Hasta que generes y subas `custom-marker.patt`, los marcadores Hiro (pista 1) y
Kanji (pista 2) van a funcionar normalmente, pero la pista 3 no va a activarse
porque AR.js no encuentra el archivo de patrón.

Cuando generes tu propio marcador con la herramienta oficial, vas a descargar
dos archivos:

1. `pattern-<algo>.patt` → renombralo a `custom-marker.patt` y guardalo en esta
   carpeta.
2. La imagen del marcador (PNG/PDF) → esa es la que hay que **imprimir**, no el
   `.patt` (el `.patt` es solo el archivo interno que usa AR.js para reconocer
   el dibujo, no se imprime).
