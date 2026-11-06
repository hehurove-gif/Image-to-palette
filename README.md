# Matiz — paletas de color

Web estática para detectar colores representativos en una imagen y crear paletas descargables.

## Uso local

Abre `index.html` en un navegador moderno. Arrastra una imagen o selecciónala, elige la cantidad de colores y pulsa **Generar paleta**. Haz clic en un color para copiar su código HEX, o descarga la paleta como archivo `.ASE`.

Todo el procesamiento se realiza localmente en el navegador; no se necesita instalación ni backend.

## Despliegue en Cloudflare Pages

El proyecto no requiere un paso de compilación. El archivo `wrangler.toml` configura el directorio raíz como salida estática de Pages.

1. Crea el proyecto de Pages en Cloudflare con el nombre `image-to-palette` (si todavía no existe).
2. Desde la raíz del repositorio, publica con Wrangler:

   ```bash
   npx wrangler pages deploy . --project-name image-to-palette
   ```

También puedes conectar el repositorio desde el panel de Cloudflare Pages y configurar `.` como directorio de salida, sin comando de build.
