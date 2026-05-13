---
title: Pausar eventos
description: Cuenta cada pausa distinta que se produjo durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 10%

---


# Pausar eventos

La métrica **Pausar eventos** cuenta cada evento `media.pauseStart` distinto recibido durante una sesión, incluidas varias pausas dentro de la misma sesión. Emparéjelo con [Duración total de la pausa](total-pause-duration.md) para obtener la longitud promedio de la pausa y con [Flujos afectados por la pausa](paused-impacted-streams.md) para contar las sesiones que se pausaron al menos una vez.

## Cálculo de esta métrica

El servidor multimedia incrementa `mediaReporting.sessionDetails.pauseCount` en cada evento `media.pauseStart`. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.pauseCount` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
