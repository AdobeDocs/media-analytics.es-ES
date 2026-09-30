---
title: Eventos de búfer (métrica)
description: Cuenta los eventos de almacenamiento en búfer para sumas y promedios entre sesiones.
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
source-wordcount: '191'
ht-degree: 7%
---

# Eventos de búfer (métrica)

>[!BEGINSHADEBOX]

*Esta página cubre la métrica **Eventos de búfer**. Adobe Analytics rellena automáticamente [eventos de búfer (dimensión)](/help/reporting/dimensions/buffer-events.md) emparejados desde la misma variable de datos de contexto `a.media.qoe.bufferCount`. Customer Journey Analytics expone un único campo `xdm.mediaReporting.qoeDataDetails.bufferCount` que puede usar como dimensión o como métrica.*

>[!ENDSHADEBOX]

La métrica **Eventos de búfer** cuenta los eventos de almacenamiento en búfer entre sesiones, lo cual es adecuado para sumas, promedios y acumulaciones de percentiles. Utilice la métrica para calcular el volumen total de búfer en un período de informe y comparar la estabilidad de búfer en contenido, redes o reproductores.

## Cálculo de esta métrica

El servidor multimedia incrementa el recuento cada vez que el reproductor entra en un estado de [inicio del búfer](/help/implementation/events/playback/buffer-start.md). La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bufferCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

Para los informes booleanos de nivel de sesión (independientemente de si la sesión experimentó almacenamiento en búfer), use [Flujos afectados por el búfer](buffer-impacted-streams.md).
