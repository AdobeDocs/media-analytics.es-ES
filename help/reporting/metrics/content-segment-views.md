---
title: Vistas de segmentos de contenido
description: Cuenta los segmentos en los que se produjo la reproducción activa del contenido principal.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 9%

---


# Vistas de segmentos de contenido

La métrica **Vistas de segmentos de contenido** cuenta segmentos de contenido de cinco minutos en los que se produjo la reproducción activa del contenido principal. La métrica confirma que el visualizador reprodujo contenido en ese segmento en lugar de solo cargar o almacenar en búfer. Emparéjelo con la dimensión [Segmento de contenido](/help/reporting/dimensions/content-segment.md) para desglosar qué partes de visualizadores de contenido de formato largo consumieron realmente.

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.sessionDetails.hasSegmentView = true` para cualquier llamada de cierre que cubra un segmento en el que se recibió al menos un evento [play](/help/implementation/events/playback/play.md) para el contenido principal. La métrica se recoge en la llamada de cierre. En la ruta de la API de Media Edge, las vistas de segmentos se activan en la misma condición que los inicios de contenido. Ambos requieren un evento [play](/help/implementation/events/playback/play.md) en el contenido principal.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.segmentView` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/A |
