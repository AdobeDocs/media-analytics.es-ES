---
title: Duración total de la pausa
description: Informa de los segundos acumulados que el visualizador ha invertido en una pausa durante una sesión.
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
source-wordcount: '164'
ht-degree: 10%
---

# Duración total de la pausa

La métrica **Duración total de la pausa** indica los segundos acumulados que el visor pasó en pausa durante una sesión. La métrica es la suma de todos los intervalos entre cada evento [pause start](/help/implementation/events/playback/pause-start.md) y el evento [play](/help/implementation/events/playback/play.md) posterior. Se agregan varias pausas. Emparejar con [eventos de pausa](pause-events.md) para derivar la longitud promedio de pausa.

## Cálculo de esta métrica

El servidor multimedia suma el tiempo de reloj de pared transcurrido entre cada evento de [inicio de pausa](/help/implementation/events/playback/pause-start.md) y el evento de [reproducción](/help/implementation/events/playback/play.md) correspondiente. La métrica se recoge en la llamada de cierre. El valor se muestra como `HH:MM:SS` en Analysis Workspace y en segundos en cualquier otra parte.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.pauseTime` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/A |
