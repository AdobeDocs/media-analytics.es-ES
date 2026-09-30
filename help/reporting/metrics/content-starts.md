---
title: El contenido comienza
description: Cuenta las sesiones en las que comenzó a reproducirse el contenido principal.
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
source-wordcount: '148'
ht-degree: 10%
---

# El contenido comienza

La métrica **Inicios de contenido** cuenta las sesiones en las que comenzó a reproducirse el contenido principal. A diferencia de [inicios de contenido](media-starts.md), excluye las sesiones que finalizaron antes de la emisión de anuncios, el almacenamiento en búfer o los bloqueos. Esto lo convierte en el denominador correcto para las tasas de finalización y participación.

## Cálculo de esta métrica

El servidor multimedia establece este indicador la primera vez que se recibe un evento [play](/help/implementation/events/playback/play.md) para el contenido principal. La métrica se activa en ese evento de reproducción, pero se comunica en la llamada de cierre. Para calcular la tasa de colocación previa a la emisión, use `(Media starts − Content starts) / Media starts`.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.play` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.play` |
