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

## Sincronizar entre celular y computador (con tu Firebase)

Como ya tienes un proyecto de Firebase, la app se conecta directo a él usando **Firestore** (base de datos en la nube, con sincronización en tiempo real):

1. Entra a tu [consola de Firebase](https://console.firebase.google.com), abre tu proyecto (el mismo del otro PWA está bien, o puedes crear uno nuevo).
2. En el menú lateral ve a **Build → Firestore Database** y créala si no existe (elige modo de producción o de prueba, cualquiera sirve para partir).
3. En **Firestore → Reglas**, por ahora déjalas así para que la app pueda leer/escribir (luego puedes restringirlas si quieres):
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /mallas/{doc} {
         allow read, write: if true;
       }
     }
   }
   ```
4. Ve a **Configuración del proyecto (ícono de tuerca) → General**, baja hasta "Tus apps", y si no tienes una app web, créala (ícono `</>`). Copia el objeto `firebaseConfig` que te muestra (algo como `{"apiKey":"...","authDomain":"...","projectId":"...", ...}`).
5. En la app, abre **⚙ Reglas**, pega ese objeto completo en "Configuración de Firebase", e inventa un "Código de tu malla" (por ejemplo `anghelo-malla`). Guarda.
6. Repite el paso 5 en tu otro dispositivo (celular o computador), con el **mismo código**.

Desde ahí, cualquier cambio que hagas (marcar un ramo, editar créditos, etc.) se guarda solo en Firebase y aparece automáticamente en tus otros dispositivos, sin tener que cerrar ni reabrir la app.

Si no configuras esto, la app sigue funcionando 100% local en el navegador (`localStorage`), solo que sin compartir entre dispositivos.

## Estructura

```
index.html      → la app completa (HTML+CSS+JS en un solo archivo)
manifest.json   → metadata de instalación (nombre, ícono, colores)
sw.js           → service worker para cache offline
icons/          → íconos de la app
```
