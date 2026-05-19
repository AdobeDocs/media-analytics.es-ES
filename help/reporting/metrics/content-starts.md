---
title: El contenido comienza
description: Cuenta las sesiones en las que comenzó a reproducirse el contenido principal.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 10%

---


# El contenido comienza

La métrica **Inicios de contenido** cuenta las sesiones en las que comenzó a reproducirse el contenido principal. A diferencia de [inicios de contenido](media-starts.md), excluye las sesiones que finalizaron antes de la emisión de anuncios, el almacenamiento en búfer o los bloqueos. Esto lo convierte en el denominador correcto para las tasas de finalización y participación.

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.sessionDetails.isPlayed = true` la primera vez que se recibe un evento [play](/help/implementation/events/playback/play.md) para el contenido principal. La métrica se activa en ese evento de reproducción, pero se comunica en la llamada de cierre. Para calcular la tasa de colocación previa a la emisión, use `(Media starts − Content starts) / Media starts`.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.play` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.play` |
