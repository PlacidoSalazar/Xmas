# LC · Landing XMAS EDIT · Prototipo V2 editorial

Prototipo HTML estático de la V2 editorial (broken grid + parallax sutil). Responsive en una sola URL, full width. Sin build.
Pensado para enseñar cómo se puede romper la grid del template actual y consultarlo con la agencia.

- `index.html` — página completa (CSS + JS inline, Lenis por CDN, fuentes de Google Fonts)
- `img/`, `video/` — assets exportados de Figma (frame "Landing Xmas Editorial")

## Qué cambia respecto a `lc-proto`
- **Broken grid** (`.grid.split`): dos columnas de 472 px (32,96 %) con margen de 123 px (8,59 %); la columna `.low` baja 200 px (13,97 %). Módulo central de 710 px entre medias. En Brillo la columna que baja es la izquierda, y el lookbook va invertido (`.lookbook.rev`).
- **Secciones** como en el Figma: Punto → foto grande → Instinto → foto grande → bloque oscuro (Brillo → foto grande → Total Black) → regalos → footer. Sin capítulo Satén.
- **Parallax**: las cards de las grids rotas (`.grid.split .card`) llegan a su sitio a distinta velocidad. Todas acaban EXACTAMENTE en su posición del Figma: solo se retrasan mientras entran por abajo y el desfase vale 0 al cruzar el 60 % del alto de pantalla (después ya no se mueven; nunca se adelantan). `--parallax:.1` en `:root` es el único valor global (la card `.low` se retrasa 0,1 × su distancia a la línea de llegada, la otra ×0,35; `0` lo apaga). Se desplaza la card entera (foto + texto), sin máscara ni escala: fotos siempre al 100 %. Usa la propiedad CSS `translate`; sin inercia propia (Lenis ya suaviza) y sin leer el DOM en cada scroll. Apagado en móvil y con `prefers-reduced-motion`.
- Mobile (≤768px): la grid asimétrica se apila en una columna, sin desfase.

## Deploy en Vercel
Proyecto propio, Root Directory = `lc-proto-editorial`, Framework: **Other**, sin build.

## Local
`npx serve .`
