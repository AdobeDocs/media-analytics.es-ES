---
title: El capítulo comienza
description: Cuenta todos los capítulos que comenzaron a reproducirse durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---


# El capítulo comienza

La métrica **Capítulos iniciados** cuenta cada capítulo que comenzó a reproducirse durante una sesión. Emparejarlo con [Capítulo completado](chapter-completes.md) para calcular la tasa de finalización del capítulo.

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.chapterDetails.isStarted = true` cuando se recibe un evento `media.chapterStart`. La métrica se recoge en la llamada de cierre del capítulo.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.chapter.view` cuando [[!UICONTROL Capítulos multimedia]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
