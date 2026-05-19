---
title: Tiempo para el inicio (métrica)
description: Notifica el tiempo de inicio para sumas y promedios entre sesiones.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 7%

---


# Tiempo para el inicio (métrica)

>[!BEGINSHADEBOX]

*Esta página cubre la métrica **Tiempo para el inicio**. Adobe Analytics rellena automáticamente un par [Tiempo para el inicio (dimensión)](/help/reporting/dimensions/time-to-start.md) desde la misma variable de datos de contexto `a.media.qoe.timeToStart`. Customer Journey Analytics expone un único campo `mediaReporting.qoeDataDetails.timeToStart` que puede usar como dimensión o como métrica. Consulte [Tiempo para el inicio](/help/implementation/variables/quality/time-to-start.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Tiempo para el inicio** indica el tiempo de inicio entre sesiones, adecuado para sumas, promedios y resúmenes de percentil. Utilice la métrica para calcular el tiempo promedio de inicio en un período de informe y comparar el rendimiento de inicio en contenido, redes o reproductores. Adobe almacena el valor en segundos y lo convierte en el momento de la ingesta a partir de los milisegundos que informa el reproductor.

## Cálculo de esta métrica

El reproductor establece `timeToStart` en el objeto QoE antes de que se active el inicio de sesión. El servidor informa del valor en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.timeToStart` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |
