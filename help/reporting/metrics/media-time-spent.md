---
title: Tiempo invertido en contenido
description: Notifica el total de segundos de reproducción activa por sesión, incluidos los anuncios.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 7%

---


# Tiempo invertido en contenido

La métrica **Tiempo invertido en contenido** indica el total de segundos de reproducción activa por sesión, incluidos el contenido principal y los anuncios, pero excluyendo las pausas, el almacenamiento en búfer y los bloqueos. Utilícela para medir el tiempo total durante el cual el visualizador interactuó activamente con el reproductor. Solo para contenido principal, usa [Tiempo invertido en contenido](content-time-spent.md).

## Cálculo de esta métrica

El servidor multimedia suma el tiempo de reloj de pared transcurrido entre los eventos mientras el reproductor se encuentra en el estado `play`, en el contenido principal o en los anuncios. Se excluye el tiempo durante las pausas, los eventos de búfer y las paradas. La métrica se recoge en la llamada de cierre. El valor se muestra como `HH:MM:SS` en Analysis Workspace y en segundos en fuentes de datos, Data Warehouse y API de informes.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.totalTimePlayed` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.totalTimePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
