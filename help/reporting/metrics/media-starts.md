---
title: Inicio de medios
description: Cuenta todas las sesiones de contenido que comenzaron, incluidas las sesiones que finalizaron en anuncios previos a la emisión o en el almacenamiento en búfer.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 6%
---

# Inicio de medios

La métrica **Inicios de medios** cuenta cada sesión de medios que comenzó. Se incrementa tan pronto como el backend recibe un evento [inicio de sesión](/help/implementation/events/session/session-start.md), incluso si el visor se cierra durante los anuncios previos a la emisión, el almacenamiento en búfer o antes de que se reproduzca cualquier contenido principal. Utilícela como la métrica de la parte superior de la funnel más amplia para informes de medios; emparéjela con [inicios de contenido](content-starts.md) para medir la entrega de anuncios y búferes.

## Cálculo de esta métrica

El servidor multimedia establece este indicador cuando se recibe un evento [inicio de sesión](/help/implementation/events/session/session-start.md). La métrica registrada es `1` por sesión. Los inicios de contenido se informan en la llamada de inicio, no en la llamada de cierre; es la única métrica que no espera el cierre de la sesión. Todas las demás métricas de contenidos, como [Inicios de contenido](/help/reporting/metrics/content-starts.md), [Tiempo invertido en contenido](/help/reporting/metrics/content-time-spent.md) y [Marcadores de progreso](/help/reporting/metrics/progress-markers.md), se registran en la llamada de cierre y no están disponibles en tiempo real durante la reproducción. [Inicios de publicidad](/help/reporting/metrics/ad-starts.md) es la única métrica adicional registrada en su evento desencadenante en lugar de en el cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.view` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.view` |
