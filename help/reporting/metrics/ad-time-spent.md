---
title: Tiempo invertido en publicidad
description: Notifica el total de segundos de reproducción de publicidad activa por sesión.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---


# Tiempo invertido en publicidad

La métrica **Tiempo invertido en publicidad** indica el total de segundos de reproducción de publicidad activa por sesión, excluyendo pausas, almacenamiento en búfer y bloqueos. Emparejarlo con [Tiempo invertido en contenido](/help/reporting/metrics/content-time-spent.md) para comparar la carga de anuncios con la participación en el contenido.

## Cálculo de esta métrica

El servidor multimedia suma el tiempo de reloj de pared transcurrido entre los eventos mientras el reproductor se encuentra en el estado `play` en un anuncio. Se excluye el tiempo durante las pausas y el almacenamiento en búfer. La métrica se recoge en la llamada de cierre del anuncio. El valor se muestra como `HH:MM:SS` en Analysis Workspace y en segundos en fuentes de datos, Data Warehouse y API de informes.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.timePlayed` cuando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
