---
title: El capítulo finaliza
description: Cuenta todos los capítulos reproducidos hasta su finalización.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 11%

---


# El capítulo finaliza

El **capítulo completado** cuenta cada capítulo que se reprodujo hasta su finalización. Emparejarlo con [inicios de capítulo](chapter-starts.md) para calcular la tasa de finalización del capítulo.

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.chapterDetails.isCompleted = true` cuando se recibe un evento `media.chapterComplete`. La métrica se recoge en la llamada de cierre del capítulo. Los capítulos omitidos o abandonados a mitad del juego no se cuentan como finalizaciones.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.chapter.complete` cuando [[!UICONTROL Capítulos multimedia]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
