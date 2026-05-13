---
title: Flujos afectados por error
description: Cuenta las sesiones en las que se produjo al menos un error.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 9%

---


# Flujos afectados por error

La métrica **Flujos afectados por el error** cuenta sesiones en las que se produjo al menos un error (`trackError` se llamó o se activó un evento `media.error`). La métrica es un booleano de nivel de sesión: varios errores dentro de la misma sesión cuentan como un flujo afectado. Para el volumen total de errores, use [Errores](/help/reporting/dimensions/errors.md).

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.qoeDataDetails.hasErrorImpactedStreams = true` la primera vez que se recibe un evento `media.error` durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.error` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
