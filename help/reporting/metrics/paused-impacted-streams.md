---
title: Flujos afectados por la pausa
description: Cuenta las sesiones en las que el visualizador se detuvo al menos una vez.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 11%

---


# Flujos afectados por la pausa

La métrica **Flujos afectados por la pausa** cuenta sesiones en las que el visor se detuvo al menos una vez. Es un booleano de nivel de sesión. Varias pausas dentro de la misma sesión cuentan como un flujo afectado. Utilícelo para medir el porcentaje de sesiones que experimentaron alguna pausa; para el volumen total de la pausa, use [Pausar eventos](pause-events.md).

## Cálculo de esta métrica

El servidor multimedia establece este indicador la primera vez que se recibe un evento [pause start](/help/implementation/events/playback/pause-start.md) durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.pause` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/A |
