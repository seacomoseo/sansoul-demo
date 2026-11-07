---
slug: videos
title: Vídeos y proporciones
sum: Vídeo local sintético para comprobar metadatos, miniaturas y proporciones.
seo:
  noindex: true
tpl:
  sections:
  - boxes:
      - title: Vídeo local con proporción original
        md: El archivo sintético mide 180 × 320 píxeles y dura un segundo. El poster usa las dimensiones del vídeo, 180 × 320. Sin ratio explícito conserva ese tamaño natural y se reduce si falta espacio.
        vid: /u/base/video-demo.mp4
        img: /u/base/poster.png
        vid_title: Vídeo local de prueba
        vid_desc: Patrón sintético de un segundo para probar el reproductor local.
  - boxes:
      - title: La misma fuente con proporción personalizada
        md: El contenedor usa 1/1; los atributos del vídeo siguen indicando 180 × 320.
        vid: /u/base/video-demo.mp4
        img: /u/base/poster.png
        ratio: 1/1
        vid_title: Vídeo local en contenedor cuadrado
        vid_desc: El mismo patrón sintético con una proporción de presentación personalizada.
---
