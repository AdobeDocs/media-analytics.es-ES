---
title: Tiempo invertido en contenido
description: Notifica el total de segundos de reproducción del contenido principal activo por sesión.
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
source-wordcount: '221'
ht-degree: 6%
---

# Tiempo invertido en contenido

La métrica **Tiempo invertido en contenido** indica el número total de segundos de reproducción del contenido principal activo por sesión, sin incluir los anuncios, las pausas, el almacenamiento en búfer y los bloqueos. Utilícelo como métrica de participación para la visualización de contenido; para ver el tiempo empleado en incluir anuncios, consulte [Tiempo invertido en contenido](media-time-spent.md).

## Cálculo de esta métrica

El servidor multimedia suma el tiempo de reloj de pared transcurrido entre los eventos mientras el reproductor se encuentra en el estado `play` en el contenido principal. Se excluye el tiempo durante los anuncios, las pausas, los eventos de búfer y los bloqueos. Como solo se cuenta el tiempo de reproducción activo, la métrica puede superar [Longitud del contenido](/help/reporting/dimensions/content-length.md) cuando un usuario hace una búsqueda hacia atrás y vuelve a ver un segmento. Cada paso a través de un segmento determinado acumula tiempo de reproducción adicional y puede acumularse durante el tiempo que el usuario consume y rebobina contenido en una sesión. La métrica se recoge en la llamada de cierre. El valor se muestra como `HH:MM:SS` en Analysis Workspace y en segundos en fuentes de datos, Data Warehouse y API de informes.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.timePlayed` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.timePlayed` |
