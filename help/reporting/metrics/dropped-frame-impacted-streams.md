---
title: Flujos afectados por fotogramas rechazados
description: Cuenta las sesiones en las que se perdió al menos un fotograma.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 11%

---


# Flujos afectados por fotogramas rechazados

**El fotograma descartado afectó a las transmisiones** sesiones de recuento de métricas en las que se descartó al menos un fotograma. La métrica es un booleano de nivel de sesión: varias caídas dentro del mismo recuento de sesiones como un flujo afectado. Para el volumen de colocación total, use [fotogramas descartados](dropped-frames.md).

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams = true` si el valor `droppedFrames` del objeto QoE es mayor que cero al cerrar la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.droppedFrames` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrames` |
