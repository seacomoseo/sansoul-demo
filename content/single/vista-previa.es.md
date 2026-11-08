---
slug: vista-previa
title: Vista previa visual de SanSoul
sum: Edita este título, resumen e imagen en Sveltia. El iframe actualiza la página real sin guardar.
img: /u/base/poster.png
seo:
  noindex: true
tpl:
  sections:
  - id: hero
    name: Presentación vinculada a los campos de página
    color: main-light
    boxes:
      - get:
          - to: title
          - from: sum
            to: md
          - to: img
        hn: h1
  - id: preview-story
    boxes:
      - title: Una sección editable
        md: Este texto se actualiza al escribir. La vista previa aproxima el Markdown de SanSoul y admite iconos, tablas y medios remotos.
        img: /u/base/poster.png
        alt: Imagen de muestra
        ratio: 16/9
  - id: preview-card
    boxes:
      - title: Una segunda sección
        md: Los campos enlazados se actualizan sin guardar. Añadir, quitar o reordenar secciones y cambiar condiciones requiere recompilar con Hugo.
        img: /u/base/icon.png
        alt: Icono de ejemplo
        ratio: 16/9
---
