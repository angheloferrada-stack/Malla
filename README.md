# Mi Malla — Ingeniería Civil Industrial (UDP)

PWA instalable para llevar el seguimiento de tu malla curricular: marcar ramos aprobados, ver qué se desbloquea, y generar un resumen de texto para pedirle análisis a una IA (semestres de atraso, qué tomar para adelantar, etc).

## Publicar en GitHub Pages (gratis)

1. Crea un repositorio nuevo en GitHub (puede ser público o privado con GitHub Pro para Pages; si es cuenta gratis, usa uno público).
2. Sube estos 5 archivos a la raíz del repo:
   - `index.html`
   - `manifest.json`
   - `sw.js`
   - `icons/icon-192.png`
   - `icons/icon-512.png`
   - (opcional) `README.md`
3. Ve a **Settings → Pages** en el repositorio.
4. En "Build and deployment", elige **Deploy from a branch**, selecciona la rama `main` y la carpeta `/ (root)`. Guarda.
5. Espera 1-2 minutos. GitHub te dará una URL tipo:
   `https://TU_USUARIO.github.io/NOMBRE_REPO/`
6. Abre esa URL desde el celular (Chrome en Android o Safari en iPhone).
7. Instálala como app:
   - **Android/Chrome**: menú (⋮) → "Añadir a pantalla de inicio" o aparecerá un aviso de instalar automáticamente.
   - **iPhone/Safari**: botón compartir (□↑) → "Añadir a pantalla de inicio".

Listo — queda como un ícono normal en tu teléfono, funciona offline (gracias al service worker) y tus datos (ramos marcados) se guardan localmente en ese navegador/dispositivo.

## Notas

- Los datos se guardan con `localStorage`, por lo tanto son **locales a cada navegador/dispositivo**. Si la abres en el computador y en el celular, no se sincronizan solas.
- Si subes cambios nuevos al repo (por ejemplo corriges un prerrequisito), quienes ya la tengan instalada verán la actualización la próxima vez que abran la app con conexión (el service worker refresca el caché).
- Para restaurar la malla original si algo queda mal editado: mantén presionado el título "Mi Malla" por un segundo.

## Estructura

```
index.html      → la app completa (HTML+CSS+JS en un solo archivo)
manifest.json   → metadata de instalación (nombre, ícono, colores)
sw.js           → service worker para cache offline
icons/          → íconos de la app
```
