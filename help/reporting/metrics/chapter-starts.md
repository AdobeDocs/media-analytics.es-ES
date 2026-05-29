---
title: El capítulo comienza
description: Cuenta todos los capítulos que comenzaron a reproducirse durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 12%

---


# El capítulo comienza

La métrica **Capítulos iniciados** cuenta cada capítulo que comenzó a reproducirse durante una sesión. Emparejarlo con [Capítulo completado](chapter-completes.md) para calcular la tasa de finalización del capítulo.

## Cálculo de esta métrica

El servidor multimedia establece este indicador cuando se recibe un evento [inicio de capítulo](/help/implementation/events/chapters/chapter-start.md). La métrica se recoge en la llamada de cierre del capítulo.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.chapter.view` cuando [[!UICONTROL Capítulos multimedia]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
