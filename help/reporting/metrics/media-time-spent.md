---
title: Tiempo invertido en contenido
description: Notifica el total de segundos de reproducción activa por sesión, incluidos los anuncios.
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
source-wordcount: '182'
ht-degree: 8%
---

# Tiempo invertido en contenido

La métrica **Tiempo invertido en contenido** indica el total de segundos de reproducción activa por sesión, incluidos el contenido principal y los anuncios, pero excluyendo las pausas, el almacenamiento en búfer y los bloqueos. Utilícela para medir el tiempo total durante el cual el visualizador interactuó activamente con el reproductor. Solo para contenido principal, usa [Tiempo invertido en contenido](content-time-spent.md).

## Cálculo de esta métrica

El servidor multimedia suma el tiempo de reloj de pared transcurrido entre los eventos mientras el reproductor se encuentra en el estado `play`, en el contenido principal o en los anuncios. Se excluye el tiempo durante las pausas, los eventos de búfer y las paradas. La métrica se recoge en la llamada de cierre. El valor se muestra como `HH:MM:SS` en Analysis Workspace y en segundos en fuentes de datos, Data Warehouse y API de informes.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.totalTimePlayed` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.totalTimePlayed`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.totalTimePlayed` |
