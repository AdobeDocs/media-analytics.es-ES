---
title: Pérdidas antes del inicio
description: Cuenta las sesiones en las que el visualizador se ha cerrado antes de que se mostrara el contenido principal.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 9%

---


# Pérdidas antes del inicio

La métrica **Pérdidas antes del inicio** cuenta las sesiones en las que el visor se cerró antes de que se procesara el contenido principal. La métrica indica el abandono previo al contenido, independientemente del comportamiento del anuncio, por lo que es la mejor medida de la entrega de contenido previo puro. Emparejarlo con [inicios de contenido](/help/reporting/metrics/media-starts.md) y [inicios de contenido](/help/reporting/metrics/content-starts.md) para calcular el porcentaje de sesiones que nunca produjeron un marco de contenido.

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.qoeDataDetails.isDroppedBeforeStart = true` para sesiones que se cierran sin producir un evento [play](/help/implementation/events/playback/play.md) en el contenido principal. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.dropBeforeStart` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.dropBeforeStart` |
