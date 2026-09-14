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

- **Mapa del Mundo multijugador** (pestaña "Mapa del Mundo"): ves el castillo de cada jugador conectado en tiempo real, con nombre y nivel, sobre el mismo sistema de cámara (arrastrar + zoom). Chat en vivo entre todos los jugadores. Requiere conectar Firebase (ver abajo) — sin conectar, funciona en **modo demostración** con castillos de ejemplo y el chat desactivado.

## Conectar el multijugador real (Firebase)

El mapa del mundo y el chat usan [Firebase](https://firebase.google.com/) (plan gratuito Spark: autenticación anónima + Firestore). Mientras no lo conectes, el juego sigue funcionando normal en modo demostración (solo "Tu Reino" y un mapa con jugadores de ejemplo).

### 1. Crear el proyecto

1. Ve a [console.firebase.google.com](https://console.firebase.google.com/) → **Crear un proyecto** (puedes desactivar Google Analytics).
2. **Compilación → Firestore Database → Crear base de datos** → cualquier ubicación → modo de prueba (test mode).
3. **Compilación → Authentication → Comenzar** → pestaña "Sign-in method" → habilita **Anónimo**.
4. **⚙️ Configuración del proyecto → Tus apps** → ícono `</>` (Web) → registra la app.
5. Copia el objeto `firebaseConfig` que te muestra.

### 2. Pegarlo en el código

En `index.html`, busca el bloque:

```js
var firebaseConfig = {
  apiKey: "PASTE_YOUR_API_KEY_HERE",
  ...
};
```

y reemplázalo por el tuyo. En cuanto `apiKey` deje de empezar con `"PASTE_"`, el juego detecta que Firebase está configurado y activa el multijugador real automáticamente (sale del modo demostración).

### 3. Reglas de seguridad (recomendado, después de las pruebas iniciales)

El modo de prueba de Firestore expira solo a los 30 días (deja de guardar datos). Antes de eso, en **Firestore Database → Reglas**, pega esto:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /players/{playerId} {
      allow read: if true;
      allow write: if request.auth != null && request.auth.uid == playerId;
    }
    match /chat/{messageId} {
      allow read: if true;
      allow create: if request.auth != null && request.resource.data.uid == request.auth.uid;
      allow update, delete: if false;
    }
  }
}
```

Esto permite que cualquiera vea el mapa y el chat, pero cada jugador solo puede escribir su propio castillo y firmar sus propios mensajes.

## Pendiente (siguientes pasos)

- Más edificios interactivos (mina de piedra, murallas, mercado) y su propio arte.
- Ambientación/tema visual definitivo (por ahora: el estilo del pack Kenney "Medieval RTS").
- Nombres propios de recursos, tropas, héroes y edificios.
- Terreno variado en el mapa del mundo (zonas, caminos), monstruos, captura de recursos, alianzas, combate.
- Balance real de costos y tiempos de construcción.
- Caminos que conecten visualmente los edificios de "Tu Reino", sonido, más animaciones.

## Stack

HTML + CSS + JS puro, sin frameworks ni build step (Firebase se carga desde su CDN oficial). Pensado para desplegar en GitHub Pages / Netlify / Vercel. Si más adelante se vuelve app nativa, se evaluará Unity o Godot.
