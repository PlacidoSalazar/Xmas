# LC · Landing XMAS EDIT · Prototipo V2 editorial

Prototipo HTML estático de la V2 editorial (broken grid + parallax sutil). Responsive en una sola URL, full width. Sin build.
Pensado para enseñar cómo se puede romper la grid del template actual y consultarlo con la agencia.

- `index.html` — página completa (CSS + JS inline, Lenis por CDN, fuentes de Google Fonts)
- `img/`, `video/` — assets exportados de Figma (frame "Landing Xmas Editorial")

## Qué cambia respecto a `lc-proto`
- **Broken grid** (`.grid.split`): dos columnas de 472 px (32,96 %) con margen de 123 px (8,59 %); la columna `.low` baja 200 px (13,97 %). Módulo central de 710 px entre medias. En Brillo la columna que baja es la izquierda, y el lookbook va invertido (`.lookbook.rev`).
- **Secciones** como en el Figma: Punto → foto grande → Instinto → foto grande → bloque oscuro (Brillo → foto grande → Total Black) → regalos → footer. Sin capítulo Satén.
- **Parallax** (solo imágenes, texto quieto): `--parallax:5` en `:root` es el único valor global (% de desplazamiento de la imagen dentro de su marco; `0` lo apaga). En cada par, la columna `.low` se mueve a ×1,35 y la otra a ×0,7 (casi el doble de diferencia). Con inercia suave (`--parallax-ease`, 0,1). En móvil va a la mitad. Se desactiva con `prefers-reduced-motion`.
- Mobile (≤768px): la grid asimétrica se apila en una columna, sin desfase.

## Deploy en Vercel
Proyecto propio, Root Directory = `lc-proto-editorial`, Framework: **Other**, sin build.

## Local
`npx serve .`
