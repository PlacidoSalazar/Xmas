# LC · Landing XMAS EDIT · Prototipo V2 editorial

Prototipo HTML estático de la V2 editorial (broken grid + parallax sutil). Responsive en una sola URL, full width. Sin build.
Pensado para enseñar cómo se puede romper la grid del template actual y consultarlo con la agencia.

- `index.html` — página completa (CSS + JS inline, Lenis por CDN, fuentes de Google Fonts)
- `img/`, `video/` — assets exportados de Figma (frame "Landing Xmas Editorial")

## Qué cambia respecto a `lc-proto`
- **Broken grid** (`.grid.split`): dos columnas de 472 px (32,96 %) con margen de 123 px (8,59 %); la columna `.low` baja 200 px (13,97 %). Módulo central de 710 px entre medias. En Brillo la columna que baja es la izquierda, y el lookbook va invertido (`.lookbook.rev`).
- **Secciones** como en el Figma: Punto → foto grande → Instinto → foto grande → bloque oscuro (Brillo → foto grande → Total Black) → regalos → footer. Sin capítulo Satén.
- **Parallax**: las cards de las grids rotas (`.grid.split .card`) se mueven a distinta velocidad. Se desplaza la card entera (foto + texto), sin máscara ni escala: las fotos siempre al 100 %. `--parallax:.08` en `:root` es el único valor global (diferencia de velocidad respecto al scroll; `0` lo apaga): la card `.low` va más lenta y la otra algo más rápida (×−0,5). Usa la propiedad CSS `translate` (independiente de `transform`); sin inercia propia (Lenis ya suaviza el scroll) y sin leer el DOM en cada scroll. Apagado en móvil y con `prefers-reduced-motion`.
- Mobile (≤768px): la grid asimétrica se apila en una columna, sin desfase.

## Deploy en Vercel
Proyecto propio, Root Directory = `lc-proto-editorial`, Framework: **Other**, sin build.

## Local
`npx serve .`
