---
title: El capítulo comienza
description: Cuenta todos los capítulos que comenzaron a reproducirse durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 13%

---


# El capítulo comienza

La métrica **Capítulos iniciados** cuenta cada capítulo que comenzó a reproducirse durante una sesión. Emparejarlo con [Capítulo completado](chapter-completes.md) para calcular la tasa de finalización del capítulo.

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.chapterDetails.isStarted = true` cuando se recibe un evento de [inicio de capítulo](/help/implementation/events/chapters/chapter-start.md). La métrica se recoge en la llamada de cierre del capítulo.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.chapter.view` cuando [[!UICONTROL Capítulos multimedia]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
