---
title: Duración total del búfer (métrica)
description: Notifica el tiempo de búfer acumulado para sumas y promedios entre sesiones.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# Duración total del búfer (métrica)

>[!BEGINSHADEBOX]

*Esta página cubre la métrica **Duración total del búfer**. Adobe Analytics rellena automáticamente un [Duración total del búfer (dimensión)](/help/reporting/dimensions/total-buffer-duration.md) emparejado desde la misma variable de datos de contexto `a.media.qoe.bufferTime`. Customer Journey Analytics expone un único campo `mediaReporting.qoeDataDetails.bufferTime` que puede usar como dimensión o como métrica.*

>[!ENDSHADEBOX]

La métrica **Duración total del búfer** indica el tiempo de búfer acumulado entre sesiones, adecuado para sumas, promedios y acumulaciones de percentiles. Utilice la métrica para calcular el tiempo total que los clientes pasan esperando en los búferes en un período de informe.

## Cálculo de esta métrica

El servidor multimedia suma la duración de cada intervalo de búfer (de `media.bufferStart` al siguiente cambio de estado). La métrica se recoge en la llamada de cierre. Analysis Workspace muestra el valor como `HH:MM:SS`; fuentes de datos, Data Warehouse y API de informes muestran el valor en segundos.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bufferTime` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
