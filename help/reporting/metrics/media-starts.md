---
title: Inicio de medios
description: Cuenta todas las sesiones de contenido que comenzaron, incluidas las sesiones que finalizaron en anuncios previos a la emisión o en el almacenamiento en búfer.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 8%

---


# Inicio de medios

La métrica **Inicios de medios** cuenta cada sesión de medios que comenzó. Se incrementa tan pronto como el backend recibe un evento [inicio de sesión](/help/implementation/events/session/session-start.md), incluso si el visor se cierra durante los anuncios previos a la emisión, el almacenamiento en búfer o antes de que se reproduzca cualquier contenido principal. Utilícela como la métrica de la parte superior de la funnel más amplia para informes de medios; emparéjela con [inicios de contenido](content-starts.md) para medir la entrega de anuncios y búferes.

## Cálculo de esta métrica

El servidor multimedia establece `mediaReporting.sessionDetails.isViewed = true` cuando se recibe un evento [inicio de sesión](/help/implementation/events/session/session-start.md). La métrica registrada es `1` por sesión. Los inicios de contenido se informan en la llamada de inicio, no en la llamada de cierre. Es la única métrica de fase 1 que no espera al cierre de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.view` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.view` |
