---
title: Control del orden de los eventos
description: Control del orden de los eventos
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 100%

---

# Control del orden de los eventos {#controlling-the-order-of-events}

Debido a que la API de recopilación de contenidos es RESTful y el seguimiento de vídeos es una operación dependiente del tiempo, es posible que le afecten las llamadas de seguimiento de API de recopilación de contenidos que llegan al back end sin orden. El proceso posterior *sí* intenta poner en cola y reordenar eventos basados en la marca de tiempo proporcionada en el objeto `playerTime`. Sin embargo, existe un límite para esta capacidad. Actualmente, la reordenación puede fallar si los retrasos entre las llamadas a un pedido son de más de un segundo. Este &quot;tiempo de demora aceptable&quot; puede optimizarse y / o configurarse en futuras actualizaciones.
