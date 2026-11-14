# Xmas · prototipos LC (Lola Casademunt)

Prototipos HTML estáticos de la landing de Navidad FW26. Sin build, sin framework. Idioma de trabajo: español (copy de la landing en español; títulos tipo "XMAS EDIT" en inglés).

## Estructura

- `lc-proto/` — V1 (la que se está revisando). No romperla: está en revisión.
- `lc-proto-editorial/` — V2 editorial (broken grid + parallax muy sutil). Copia de `lc-proto` como base.
- Cada carpeta es un proyecto de Vercel independiente (Framework: Other, sin build); su **Root Directory** es la carpeta. Cada una tiene su `index.html` (CSS y JS inline), `img/`, `video/` y `vercel.json`.
- Los assets (`img/`, `video/`) se exportan desde Figma y se suben tal cual. Los assets compartidos se duplican en cada carpeta (Vercel solo sirve lo que hay bajo su Root Directory).
- Push directo a `main`; Vercel despliega solo.

## Caché (importante)

`vercel.json` sirve `/img` y `/video` con `Cache-Control: immutable, max-age=1 año`. Si **reemplazas** una imagen con el mismo nombre, el navegador (sobre todo Safari iPhone) seguirá mostrando la vieja. Sube siempre `?v=N` en TODOS los usos de esa imagen en el `index.html` (patrón ya usado: `img/feat-2-m.jpg?v=2`) o usa un nombre nuevo. Comprueba también que las imágenes no traigan bordes de 1px de color (pasó con `brillo-p1.jpg`).

## Responsive

Una sola URL: desktop con `max-width:1432px` centrado; mobile con `@media (max-width:768px)` (Figma "Landing Mobile Final", 360). Hero/feature/look tienen variante mobile con `<picture>` y sufijo `-m.jpg`.

## Tokens (la fuente de verdad es Figma; el CSS los refleja en `:root`)

Spacing = colección Figma **LC · Spacing** (modos Desktop | Mobile):

| CSS | Figma | Desktop | Mobile |
|---|---|---|---|
| `--gap` | `space/chapter` | 140 | 64 |
| `--block-gap` | `space/block` | 80 | 36 |
| `--heading-gap` | `space/heading` | 8 | 8 |

El resto (`--inset`, `--gutter`, `--text-inset`) viene de **LC · Spatial**. Tipografía: colección **LC · Typography** (Desktop | Mobile). Si cambia un valor en Figma, cambiar también el `:root` y el override mobile (`@media`) del CSS.

## Motion

- `--tempo:.9` multiplica todas las duraciones (escala musical, tónica .4s). Easings: `--ease` (UI) y `--soft` (atmósfera, reveals).
- Smooth scroll con Lenis 1.1.20 (CDN), parallax con `data-parallax`, preloader/shimmer vía clase `.ready`.
- Respetar `prefers-reduced-motion`. V2 editorial: parallax **muy minimal** (solo imágenes, ~4-6 %, dentro del marco; texto quieto; en mobile apagado o a la mitad; un único valor global ajustable).

## Figma

Archivo "LC · Soft Christmas FW26 · Landing" (fileKey `39pGeaJxChfDQm0gGZsPaD`). Frames: `Landing Xmas Final` (desktop) y `Landing Mobile Final` (mobile). Los frames tienen los modos de variables fijados (Desktop / Mobile).

## Convenciones

- Cambios pequeños y concretos; no reescribir el HTML entero.
- Commit en español, claro y corto. Push a `main` solo cuando el usuario lo pida.
- Tras cambios visuales, recordar probar en iPhone Safari (pestaña privada si hay caché).
