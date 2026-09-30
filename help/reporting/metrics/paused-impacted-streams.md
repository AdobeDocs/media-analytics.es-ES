---
title: Flujos afectados por la pausa
description: Cuenta las sesiones en las que el visualizador se detuvo al menos una vez.
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
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/A |
