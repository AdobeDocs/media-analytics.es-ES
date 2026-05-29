---
title: Tiempo dedicado al capítulo
description: Notifica el total de segundos de reproducción activa por capítulo.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 9%

---


# Tiempo dedicado al capítulo

La métrica **Tiempo invertido en el capítulo** indica el total de segundos de reproducción activa por capítulo. Emparejarlo con [Chapter length](/help/reporting/dimensions/chapter-length.md) para calcular el porcentaje de cada capítulo consumido.

## Cálculo de esta métrica

El servidor multimedia suma el tiempo de reloj de pared transcurrido entre los eventos mientras el reproductor se encuentra en el estado `play` en un capítulo. Se excluye el tiempo durante las pausas, el almacenamiento en búfer y las paradas. La métrica se recoge en la llamada de cierre del capítulo. El valor se muestra como `HH:MM:SS` en Analysis Workspace y en segundos en fuentes de datos, Data Warehouse y API de informes.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.chapter.timePlayed` cuando [[!UICONTROL Capítulos multimedia]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.timePlayed`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.timePlayed` |
