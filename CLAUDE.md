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

Una sola URL, **full width** (como Loewe): sin tope de ancho (`--page-max:none`; para limitar, p. ej. `1920px`, y se centra). Mobile con `@media (max-width:768px)` (Figma "Landing Mobile Final", 360). Hero/feature/look tienen variante mobile con `<picture>` y sufijo `-m.jpg`.

- La grid va en porcentajes (`32,96 %` = 472/1432, `49,58 %` = 710/1432) y `aspect-ratio`; así escala sola con la ventana.
- Hero: `aspect-ratio:1432/810`, `max-height:100svh`, texto al `78,6 %`. En mobile se vuelve `height:640px`.
- Spacing: `--gap` y `--block-gap` usan `clamp()`: 140 y 80 hasta 1432 y crecen hasta 188 y 107 en 1920 (mobile: 64 y 36, fijos).
- Ribbon superior: HTML con texto real (Manrope 14px; 12px en mobile) y flechas/cierre en SVG. No volver a la imagen `topbar.png`: `object-fit:cover` la amplía a ancho completo.
- Texto e iconos son fijos de momento; las alturas de los pies de producto (px) no escalan.

## Tokens (la fuente de verdad es Figma; el CSS los refleja en `:root`)

Spacing = colección Figma **LC · Spacing** (modos Desktop | Mobile):

| CSS | Figma | Desktop | Mobile |
|---|---|---|---|
| `--gap` | `space/chapter` | 140 | 64 |
| `--block-gap` | `space/block` | 80 | 36 |
| `--heading-gap` | `space/heading` | 8 | 8 |

El resto (`--inset`, `--gutter`, `--text-inset`) viene de **LC · Spatial**. Tipografía: colección **LC · Typography** (Desktop | Mobile). Si cambia un valor en Figma, cambiar también el `:root` y el override mobile (`@media`) del CSS.

## Tipografía fluida (pendiente)

Plan: cada nivel tiene su mínimo (el actual) y su máximo a partir de 1920, con `clamp()` y `rem` + `vw` (respeta el zoom). Ejemplo para 14→16 entre 1432 y 1920: `clamp(0.875rem, 0.508rem + 0.41vw, 1rem)`. Propuesta inicial (a revisar a ojo): hero título 24→28, título de capítulo 20→24, cuerpo/descripción/banner/precio 14→16, nombre de producto 13→15, tag 12→13. Los pequeños escalan menos para no perder jerarquía. Llevarlo también a LC · Typography en Figma (modo Desktop + modo XL).

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
