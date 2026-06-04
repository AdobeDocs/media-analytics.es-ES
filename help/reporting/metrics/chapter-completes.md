---
title: El capítulo finaliza
description: Cuenta todos los capítulos reproducidos hasta su finalización.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 12%

---


# El capítulo finaliza

El **capítulo completado** cuenta cada capítulo que se reprodujo hasta su finalización. Emparejarlo con [inicios de capítulo](chapter-starts.md) para calcular la tasa de finalización del capítulo.

## Cálculo de esta métrica

El servidor multimedia establece este indicador cuando se recibe un evento [capítulo completado](/help/implementation/events/chapters/chapter-complete.md). La métrica se recoge en la llamada de cierre del capítulo. Los capítulos omitidos o abandonados a mitad del juego no se cuentan como finalizaciones.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.chapter.complete` cuando [[!UICONTROL Capítulos multimedia]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.complete` |
