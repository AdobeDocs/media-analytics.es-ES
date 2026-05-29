---
title: Tiempo de reproducción única
description: Notifica los segundos de contenido distinto vistos durante una sesión, lo que anula la duplicación de las reproducciones seek-back.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# Tiempo de reproducción única

La métrica **Tiempo único reproducido** indica los segundos de contenido distinto visualizado durante una sesión, lo que anula la duplicación de segmentos que se reprodujeron mediante recuperación. En comparación con [Tiempo invertido en contenido](content-time-spent.md), el tiempo de reproducción único es menor cuando un usuario vuelve a ver una parte del mismo contenido dentro de la misma sesión.

## Cálculo de esta métrica

El back-end de medios rastrea qué intervalos de cabezal de reproducción se han visto durante la sesión y suma su unión. Reproducir el mismo segmento de cinco segundos dos veces sigue contando como cinco segundos. La métrica se recoge en la llamada de cierre. El valor se muestra como `HH:MM:SS` en Analysis Workspace y en segundos en fuentes de datos, Data Warehouse y API de informes.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.uniqueTimePlayed` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.uniqueTimePlayed`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.uniqueTimePlayed` |
