# Contenido de referencia

La demo ofrece rutas para inicio, blog, servicios, productos, eventos, componentes y divisores. Los índices y fichas ficticias de colecciones usan `seo.noindex: true`; la página de componentes también es técnica y no debe indexarse. El inicio identifica el sitio como una referencia de SanSoul.

| Ruta | Cobertura visible |
| --- | --- |
| `/` | Hero, introducción, lista de servicios, pasos, galería local, entradas recientes, FAQ, reseñas, formulario y mapa neutro. |
| `/blog/` | Markdown, fechas históricas, autoría y categorías enlazadas. |
| `/servicios/` | Fichas relacionadas con tarjetas y precios ficticios. |
| `/productos/` | Ficha con precio, stock, marca, fabricante y categoría ficticios. |
| `/eventos/` | Evento histórico ficticio con fechas y ubicación descrita como demostrativa. |
| `/componentes/` | Cajas, acciones, pasos, galería, preguntas, reseñas, formulario, mapa y modal. |
| `/videos/` | Archivo sintético local de un segundo, proporción vertical original y presentación cuadrada. |
| `/vista-previa/` | Página sencilla para probar la vista previa experimental de Sveltia sin guardar cambios. |
| `/preview-estructural/` | Borrador local con condición en Resumen, `get` y `remap`, sin guardar. |
| `/espaciado-y-pips/` | Márgenes adaptables de cajas/bloques/botones, ancho de acción automático o forzado, enlaces con `set`/`remap`, indicadores `pill`, acciones circulares y horarios. |
| `/calendario/` | Calendario de eventos ficticios de varios días, solapamientos, continuidad entre semanas/meses, título largo completo, sesión de un día, año de doce meses, mes compacto móvil y detalle de eventos por día. |
| `/carrusel-infinito/` | Continuidad con ocho tarjetas originales y caso finito por falta de elementos. |
| `/divisores/` | Galería de separadores del tema. |

Las imágenes apuntan a recursos locales de `uploads/base/`. Los formularios muestran validación, pero su acción es `about:blank` y la dirección de correo usa el dominio reservado `example.com`; no están conectados a un proveedor de envío. El mapa muestra coordenadas neutrales `[0, 0]`. No incluyas datos personales ni uses estos valores como información de una organización real. La configuración no incluye un identificador GA4. `cookies_legal: false` es deliberado: las integraciones configuradas no esperan consentimiento. Cada proyecto puede activar `true` para exigirlo.

Al crear un proyecto, conserva solo las páginas y los tipos de contenido que necesites, reemplaza sus datos ficticios y actualiza el menú. Para el catálogo amplio de parámetros y la guía de copia, consulta [los ejemplos canónicos del tema](../core/_examples/README.md).

El vídeo de `uploads/base/video-demo.mp4` es un patrón generado para pruebas,
sin audio ni imágenes de personas. La vista previa experimental está activada en las colecciones de contenido; véase [su alcance y uso](../core/docs/cms-live-preview.md).
