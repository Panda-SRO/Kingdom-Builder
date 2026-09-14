# Kingdom Builder

Prototipo web de un juego de estrategia de construcción de base (estilo Lord Mobile / Clash of Clans / Rise of Kingdoms en mecánica — sin copiar arte ni nombres). Proyecto original, en fase temprana de prototipo jugable.

## Cómo probarlo

Es un único archivo HTML sin dependencias de build. Puedes abrirlo directamente:

```bash
start index.html    # o doble click en index.html
```

O publicarlo en GitHub Pages (Settings → Pages → Deploy from a branch → `main` / `root`) para compartir el link con amigos desde el celular o la compu.

## Qué incluye este prototipo

- Vista de ciudad con 4 edificios: Castillo (nv. 5), Granja (nv. 3), Aserradero (nv. 2), Cuartel (nv. 4).
- Barra de recursos: oro, madera, piedra.
- Al tocar un edificio se abre un panel con su nivel actual, descripción y costo de mejora.
- Botón de mejora que descuenta recursos, sube el nivel y aumenta el costo de la siguiente mejora (+30%).
- Validación de recursos insuficientes (el botón se deshabilita y muestra qué falta).
- Progreso guardado en el navegador (`localStorage`) — persiste entre recargas. Botón "Reiniciar progreso" al pie de la página.

## Pendiente (siguientes pasos)

- Producción pasiva de recursos por tiempo (granja → oro, aserradero → madera, mina → piedra).
- Ambientación/tema visual definitivo (por ahora: medieval clásico, oro y piedra oscura).
- Nombres propios de recursos, tropas, héroes y edificios.
- Mapa mundial, alianzas, investigación, eventos temporales (ver alcance completo del proyecto).
- Balance real de costos y tiempos de construcción.
- Arte propio (placeholders actuales: emojis) o arte generado/contratado.

## Stack

HTML + CSS + JS puro, sin frameworks ni build step. Pensado para desplegar en GitHub Pages / Netlify / Vercel. Si más adelante se vuelve app nativa, se evaluará Unity o Godot.
