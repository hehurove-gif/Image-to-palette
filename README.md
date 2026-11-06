# Matiz — paletas de color

Web estática para detectar colores representativos en una imagen y crear paletas descargables.

## Uso local

Abre `index.html` en un navegador moderno. Arrastra una imagen o selecciónala, elige la cantidad de colores y pulsa **Generar paleta**. Haz clic en un color para copiar su código HEX, o descarga la paleta como archivo `.ASE`.

Todo el procesamiento se realiza localmente en el navegador; no se necesita instalación ni backend.

## Cómo se eligen los colores

- Se agrupan los píxeles en el espacio de color Lab (más cercano a cómo percibimos el color) y se devuelven colores que realmente existen en la imagen, no mezclas.
- Se ignoran los bordes suavizados entre zonas, que generan colores falsos.
- Los colores casi idénticos se fusionan: si la imagen solo tiene 3 colores distintos, verás 3 y no 5 repetidos.
- Los degradados suaves se detectan aparte y la paleta se reparte de un extremo al otro.
- El archivo `.ASE` (Adobe Swatch Exchange) abre en Photoshop, Illustrator, InDesign y Affinity.

## Despliegue en Cloudflare Pages

El proyecto no requiere un paso de compilación. El archivo `wrangler.toml` configura el directorio raíz como salida estática de Pages.

1. Crea el proyecto de Pages en Cloudflare con el nombre `image-to-palette` (si todavía no existe).
2. Desde la raíz del repositorio, publica con Wrangler:

   ```bash
   npx wrangler pages deploy . --project-name image-to-palette
   ```

También puedes conectar el repositorio desde el panel de Cloudflare Pages y configurar `.` como directorio de salida, sin comando de build.
