---
seo-title: Control del orden de los eventos
title: Control del orden de los eventos
uuid: 007 fccc 6-be 72-4 b 79-826 d -588 c 957 ccf 15
translation-type: tm+mt
source-git-commit: 6e13e9a6250949a3a7f059445da772b4db1fdb71

---


# Control del orden de los eventos{#controlling-the-order-of-events}

Debido a que la API de recopilación de medios es restful y el seguimiento de vídeo es una operación que depende mucho del tiempo, es posible que un implementador le pregunte si las llamadas de seguimiento de la API de Media Collection llegan al final del pedido. El proceso posterior *sí* intenta poner en cola y reordenar eventos basados en la marca de tiempo proporcionada en el objeto `playerTime`. Sin embargo, existe un límite para esta capacidad. Actualmente, la reordenación puede fallar si los retrasos entre las llamadas a un pedido son de más de un segundo. Este "tiempo de demora aceptable" puede optimizarse y / o configurarse en futuras actualizaciones.
