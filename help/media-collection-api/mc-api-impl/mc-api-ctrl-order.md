---
title: Control del orden de los eventos
description: null
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Control del orden de los eventos {#controlling-the-order-of-events}

Debido a que la API de recopilación de contenidos es RESTful y el seguimiento de vídeos es una operación dependiente del tiempo, es posible que le afecten las llamadas de seguimiento de API de recopilación de contenidos que llegan al back end sin orden. El proceso posterior *sí* intenta poner en cola y reordenar eventos basados en la marca de tiempo proporcionada en el objeto `playerTime`. Sin embargo, existe un límite para esta capacidad. Actualmente, la reordenación puede fallar si los retrasos entre las llamadas a un pedido son de más de un segundo. Este "tiempo de demora aceptable" puede optimizarse y / o configurarse en futuras actualizaciones.
