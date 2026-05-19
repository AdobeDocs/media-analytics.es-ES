---
title: Flujos afectados por cambio de velocidad
description: Cuenta las sesiones en las que se produjo al menos un cambio en la velocidad de bits.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 10%

---


# Flujos afectados por cambio de velocidad

El cambio de **velocidad de bits afectó a flujos** sesiones de recuento de métricas en las que se produjo al menos un cambio de velocidad de bits. La métrica es un booleano de nivel de sesión: varios cambios de velocidad de bits dentro del mismo recuento de sesiones como un flujo afectado. Para el volumen total de cambio de velocidad de bits, use [Cambios de velocidad de bits](/help/reporting/dimensions/bitrate-changes.md).

## Cálculo de esta métrica

El servidor multimedia establece este indicador la primera vez que se recibe un evento de [cambio en la velocidad de bits](/help/implementation/events/playback/bitrate-change.md) durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bitrateChange` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChange` |
