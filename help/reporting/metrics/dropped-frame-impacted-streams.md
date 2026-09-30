---
title: Flujos afectados por fotogramas rechazados
description: Cuenta las sesiones en las que se perdió al menos un fotograma.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 11%
---

# Flujos afectados por fotogramas rechazados

**El fotograma descartado afectó a las transmisiones** sesiones de recuento de métricas en las que se descartó al menos un fotograma. La métrica es un booleano de nivel de sesión; varias caídas dentro de la misma sesión cuentan como un flujo afectado. Para el volumen de colocación total, use [fotogramas descartados](dropped-frames.md).

## Cálculo de esta métrica

El servidor multimedia establece este indicador si el valor `droppedFrames` del objeto QoE es mayor que cero al cerrar la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.droppedFrames` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrames` |
