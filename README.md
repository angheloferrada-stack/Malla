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

- Si subes cambios nuevos al repo (por ejemplo corriges un prerrequisito), quienes ya la tengan instalada verán la actualización la próxima vez que abran la app con conexión (el service worker refresca el caché).
- Para restaurar la malla original si algo queda mal editado: mantén presionado el título "Mi Malla" por un segundo.

## Semestre automático según año de ingreso

En **⚙ Reglas** ingresa tu año de ingreso (ej. 2024). La app calcula sola:
- **Semestre según ingreso**: dónde deberías ir si no llevaras atraso, contando desde marzo de ese año (2 semestres por año).
- **Semestre aprox. real**: se estima según los ramos marcados como "cursando" (usa el semestre de la malla donde más ramos estás cursando); si no marcaste ninguno, lo estima con tus créditos aprobados.
- **Semestres de atraso**: la diferencia entre ambos.

## Sincronizar entre celular y computador

Por defecto los datos se guardan solo en el navegador de cada dispositivo (`localStorage`). Para que se vean iguales en el celular y el computador, la app puede sincronizar contra un "bin" gratuito de **jsonbin.io**:

1. Crea una cuenta gratis en https://jsonbin.io
2. Ve a **API Keys** → "Create Access Key", dale un nombre, y marca los permisos de Bins (create, read, update). Copia esa clave.
3. En la app, abre **⚙ Reglas**, pega la clave en "Clave de API (jsonbin.io Master Key)" y toca **Crear**. Esto genera un "Código de sincronización" (el ID del bin).
4. Guarda los cambios. Copia ese código (y la misma clave) y pégalos en el mismo panel del otro dispositivo (por ejemplo tu celular), luego guarda ahí también.
5. Desde ese momento, cada vez que marques un ramo como aprobado/cursando en un dispositivo, se sube automáticamente; y al abrir la app en el otro dispositivo (o volver a la pestaña), trae los datos más recientes.

Si no configuras esto, la app sigue funcionando 100% offline y local, solo que cada dispositivo tendrá su propia copia.

## Estructura

```
index.html      → la app completa (HTML+CSS+JS en un solo archivo)
manifest.json   → metadata de instalación (nombre, ícono, colores)
sw.js           → service worker para cache offline
icons/          → íconos de la app
```
