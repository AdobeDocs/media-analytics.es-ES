---
title: Duración total del búfer (métrica)
description: Notifica el tiempo de búfer acumulado para sumas y promedios entre sesiones.
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
source-wordcount: '196'
ht-degree: 7%
---

# Duración total del búfer (métrica)

>[!BEGINSHADEBOX]

*Esta página cubre la métrica **Duración total del búfer**. Adobe Analytics rellena automáticamente un [Duración total del búfer (dimensión)](/help/reporting/dimensions/total-buffer-duration.md) emparejado desde la misma variable de datos de contexto `a.media.qoe.bufferTime`. Customer Journey Analytics expone un único campo `xdm.mediaReporting.qoeDataDetails.bufferTime` que puede usar como dimensión o como métrica.*

>[!ENDSHADEBOX]

La métrica **Duración total del búfer** indica el tiempo de búfer acumulado entre sesiones, adecuado para sumas, promedios y acumulaciones de percentiles. Utilice la métrica para calcular el tiempo total que los clientes pasan esperando en los búferes en un período de informe.

## Cálculo de esta métrica

El servidor multimedia suma la duración de cada intervalo de búfer (desde [inicio del búfer](/help/implementation/events/playback/buffer-start.md) hasta el siguiente cambio de estado). La métrica se recoge en la llamada de cierre. Analysis Workspace muestra el valor como `HH:MM:SS`; fuentes de datos, Data Warehouse y API de informes muestran el valor en segundos.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bufferTime` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |
