---
title: Tiempo invertido en publicidad
description: Notifica el total de segundos de reproducción de publicidad activa por sesión.
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
source-wordcount: '174'
ht-degree: 8%
---

# Tiempo invertido en publicidad

La métrica **Tiempo invertido en publicidad** indica el total de segundos de reproducción de publicidad activa por sesión, excluyendo pausas, almacenamiento en búfer y bloqueos. Emparejarlo con [Tiempo invertido en contenido](/help/reporting/metrics/content-time-spent.md) para comparar la carga de anuncios con la participación en el contenido.

## Cálculo de esta métrica

El servidor multimedia suma el tiempo de reloj de pared transcurrido entre los eventos mientras el reproductor se encuentra en el estado `play` en un anuncio. Se excluye el tiempo durante las pausas, el almacenamiento en búfer y las búsquedas, de acuerdo con la forma en que se calcula el [Tiempo invertido en contenido](/help/reporting/metrics/content-time-spent.md) para el contenido principal. La métrica se recoge en la llamada de cierre del anuncio. El valor se muestra como `HH:MM:SS` en Analysis Workspace y en segundos en fuentes de datos, Data Warehouse y API de informes.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.timePlayed` cuando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.timePlayed` |
