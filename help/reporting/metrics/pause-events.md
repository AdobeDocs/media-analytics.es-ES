---
title: Pausar eventos
description: Cuenta cada pausa distinta que se produjo durante una sesión.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---


# Pausar eventos

La métrica **Pause events** cuenta cada evento [pause start](/help/implementation/events/playback/pause-start.md) distinto recibido durante una sesión, incluidas varias pausas dentro de la misma sesión. Emparéjelo con [Duración total de la pausa](total-pause-duration.md) para obtener la longitud promedio de la pausa y con [Flujos afectados por la pausa](paused-impacted-streams.md) para contar las sesiones que se pausaron al menos una vez.

## Cálculo de esta métrica

El servidor multimedia incrementa este recuento en cada evento [inicio de pausa](/help/implementation/events/playback/pause-start.md). Una sola pausa continua genera un incremento independientemente de su duración. Los [pings](/help/implementation/events/playback/ping.md) de latido enviados mientras el reproductor permanece en pausa pertenecen al mismo período de pausa y no se vuelve a incrementar el recuento. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.pauseCount` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/A |
