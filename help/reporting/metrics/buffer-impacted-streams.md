---
title: Flujos afectados por búfer
description: Cuenta las sesiones en las que el reproductor ha entrado en un estado de búfer al menos una vez.
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
source-wordcount: '147'
ht-degree: 10%
---

# Flujos afectados por búfer

La métrica **Flujos afectados por el búfer** cuenta las sesiones en las que el reproductor entró en un estado de búfer al menos una vez. La métrica es un booleano de nivel de sesión; varios eventos de búfer dentro de la misma sesión cuentan como un flujo afectado. Para el volumen total de búfer, use [Eventos de búfer](buffer-events.md).

## Cálculo de esta métrica

El servidor multimedia establece este indicador la primera vez que se recibe un evento [inicio del búfer](/help/implementation/events/playback/buffer-start.md) durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.buffer` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.buffer` |
