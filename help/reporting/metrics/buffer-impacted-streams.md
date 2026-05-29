---
title: Flujos afectados por búfer
description: Cuenta las sesiones en las que el reproductor ha entrado en un estado de búfer al menos una vez.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 10%

---


# Flujos afectados por búfer

La métrica **Flujos afectados por el búfer** cuenta las sesiones en las que el reproductor entró en un estado de búfer al menos una vez. La métrica es un booleano de nivel de sesión: varios eventos de búfer dentro de la misma sesión cuentan como un flujo afectado. Para el volumen total de búfer, use [Eventos de búfer](buffer-events.md).

## Cálculo de esta métrica

El servidor multimedia establece este indicador la primera vez que se recibe un evento [inicio del búfer](/help/implementation/events/playback/buffer-start.md) durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.buffer` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.buffer` |
