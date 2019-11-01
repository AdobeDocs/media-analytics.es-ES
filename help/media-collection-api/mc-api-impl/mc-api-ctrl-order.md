---
title: Control del orden de los eventos
description: null
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Control del orden de los eventos{#controlling-the-order-of-events}

Dado que la API de recopilación de medios es RESTful y el seguimiento de vídeo depende en gran medida del tiempo, un implementador podría preocuparse por las llamadas de seguimiento de la API de recopilación de medios que llegan al servidor en orden. El proceso posterior *sí* intenta poner en cola y reordenar eventos basados en la marca de tiempo proporcionada en el objeto `playerTime`. Sin embargo, existe un límite para esta capacidad. Actualmente, la reordenación puede fallar si los retrasos entre las llamadas a un pedido son de más de un segundo. Este "tiempo de demora aceptable" puede optimizarse y / o configurarse en futuras actualizaciones.
