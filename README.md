# Kingdom Builder

Prototipo web de un juego de estrategia de construcción de base (estilo / Castillos en mecánica — sin copiar arte ni nombres). Proyecto original, en fase temprana de prototipo jugable.

## Cómo probarlo

Es un único archivo HTML sin dependencias de build. Puedes abrirlo directamente:

```bash
start index.html    # o doble click en index.html
```

O publicarlo en GitHub Pages (Settings → Pages → Deploy from a branch → `main` / `root`) para compartir el link con amigos desde el celular o la compu.

## Qué incluye este prototipo

- Mapa del reino con cámara: arrastra para moverte, pellizca (móvil) o rueda del mouse / botones +/− para hacer zoom.
- Arte real de videojuego (pack "Medieval RTS" de Kenney.nl, CC0 — ver `assets/CREDITS.txt`): Castillo (nv. 5), Granja (nv. 3), Aserradero (nv. 2), Cuartel (nv. 4), más casas, árboles y rocas decorativas para dar sensación de pueblo poblado.
- Barra de recursos: oro, madera, piedra, con iconos propios en SVG.
- Producción pasiva de recursos: la Granja genera oro y el Aserradero madera automáticamente con el tiempo, incluso mientras no tienes la página abierta (al volver, un aviso muestra cuánto ganaste).
- Al tocar un edificio se abre un panel con su nivel actual, descripción, producción (si aplica) y costo de mejora.
- Botón de mejora que descuenta recursos, sube el nivel y aumenta el costo de la siguiente mejora (+30%), con animación de "pop" y partículas de polvo.
- Validación de recursos insuficientes (el botón se deshabilita y muestra qué falta).
- Progreso guardado en el navegador (`localStorage`) — persiste entre recargas. Botón "Reiniciar progreso" al pie de la página.

## Pendiente (siguientes pasos)

- Más edificios interactivos (mina de piedra, murallas, mercado) y su propio arte.
- Ambientación/tema visual definitivo (por ahora: el estilo del pack Kenney "Medieval RTS").
- Nombres propios de recursos, tropas, héroes y edificios.
- Mapa mundial, alianzas, investigación, eventos temporales (ver alcance completo del proyecto).
- Balance real de costos y tiempos de construcción.
- Caminos que conecten visualmente los edificios, sonido, más animaciones.

## Stack

HTML + CSS + JS puro, sin frameworks ni build step. Pensado para desplegar en GitHub Pages / Netlify / Vercel. Si más adelante se vuelve app nativa, se evaluará Unity o Godot.
