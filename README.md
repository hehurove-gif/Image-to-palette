# Matiz — paletas de color

Web estática para detectar colores representativos en una imagen y crear paletas descargables.

## Uso local

Abre `public/index.html` en un navegador moderno. Arrastra una imagen o selecciónala, elige la cantidad de colores y pulsa **Generar paleta**. Haz clic en un color para copiar su código HEX, o descarga la paleta como archivo `.ASE`.

Todo el procesamiento se realiza localmente en el navegador; no se necesita instalación ni backend.

## Cómo se eligen los colores

- Se agrupan los píxeles en el espacio de color Lab (más cercano a cómo percibimos el color) y se devuelven colores que realmente existen en la imagen, no mezclas.
- Se ignoran los bordes suavizados entre zonas, que generan colores falsos.
- Los colores casi idénticos se fusionan: si la imagen solo tiene 3 colores distintos, verás 3 y no 5 repetidos.
- Los degradados suaves se detectan aparte y la paleta se reparte de un extremo al otro.
- El archivo `.ASE` (Adobe Swatch Exchange) abre en Photoshop, Illustrator, InDesign y Affinity.

## Despliegue en Cloudflare (Workers)

El sitio es un solo archivo (`public/index.html`) y se sirve como Worker con archivos estáticos (`wrangler.jsonc`). No hay paso de compilación. Conecta el repositorio desde Cloudflare (Workers → Create → Import a repository) con estos valores:

| Campo | Valor |
|---|---|
| Nombre del Worker | `image-to-palette` |
| Build command | *(vacío)* |
| Deploy command | `npx wrangler deploy` |

Cada push a la rama principal despliega solo.

## Cuando `hetor.dev` esté en Cloudflare (hetor.dev/tools/palette)

1. En Cloudflare → Worker `image-to-palette` → Settings → Build: Deploy command `npx wrangler deploy -c wrangler.domain.jsonc`.
2. Lanza un nuevo despliegue. La ruta `hetor.dev/tools/palette*` tiene prioridad sobre el Worker de Hetor.

No hace falta variable de base: la página no usa rutas absolutas.
