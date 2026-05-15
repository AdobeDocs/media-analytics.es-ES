---
title: Flujos afectados por estancamiento
description: Cuenta las sesiones en las que se produjo al menos una detención durante la reproducción.
feature: Metrics
role: User, Admin
source-git-commit: 1278355e0bfc67c635250c426edaf865fb658c37
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 8%

---


# Flujos afectados por estancamiento

La métrica **Stall’ afectó a los flujos** y cuenta las sesiones en las que se produjo al menos una detención durante la reproducción. La métrica es un booleano de nivel de sesión: varias interrupciones dentro del mismo recuento de sesiones como un flujo afectado. Para el volumen de detención total, use [Eventos de detención](stall-events.md).

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.qoeDataDetails.hasStallImpactedStreams = true` cuando no se registra ningún movimiento del cabezal de reproducción en el contenido principal durante al menos tres eventos consecutivos durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.qoe.stall` a un evento personalizado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasStallImpactedStreams`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (el evento personalizado al que la regla de procesamiento asigna `a.media.qoe.stall`; consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stall` |
