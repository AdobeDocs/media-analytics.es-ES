---
title: Tiempo de reproducción única
description: Notifica los segundos de contenido distinto vistos durante una sesión, lo que anula la duplicación de las reproducciones seek-back.
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
source-wordcount: '180'
ht-degree: 8%
---

# Tiempo de reproducción única

La métrica **Tiempo único reproducido** indica los segundos de contenido distinto visualizado durante una sesión, lo que anula la duplicación de segmentos que se reprodujeron mediante recuperación. En comparación con [Tiempo invertido en contenido](content-time-spent.md), el tiempo de reproducción único es menor cuando un usuario vuelve a ver una parte del mismo contenido dentro de la misma sesión.

## Cálculo de esta métrica

El back-end de medios rastrea qué intervalos de cabezal de reproducción se han visto durante la sesión y suma su unión. Reproducir el mismo segmento de cinco segundos dos veces sigue contando como cinco segundos. La métrica se recoge en la llamada de cierre. El valor se muestra como `HH:MM:SS` en Analysis Workspace y en segundos en fuentes de datos, Data Warehouse y API de informes.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.uniqueTimePlayed` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.uniqueTimePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.uniqueTimePlayed` |
