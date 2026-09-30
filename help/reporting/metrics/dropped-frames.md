---
title: Fotogramas perdidos (métrica)
description: Informa de los fotogramas perdidos acumulados para sumas y promedios entre sesiones.
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
source-wordcount: '200'
ht-degree: 7%
---

# Fotogramas perdidos (métrica)

>[!BEGINSHADEBOX]

*Esta página cubre la métrica **fotogramas perdidos**. Adobe Analytics rellena automáticamente un par de [fotogramas perdidos (dimensión)](/help/reporting/dimensions/dropped-frames.md) desde la misma variable de datos de contexto `a.media.qoe.droppedFrameCount`. Customer Journey Analytics expone un único campo `xdm.mediaReporting.qoeDataDetails.droppedFrames` que puede usar como dimensión o como métrica. Consulte [Fotogramas perdidos](/help/implementation/variables/quality/dropped-frames.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Fotogramas perdidos** indica fotogramas perdidos acumulados entre sesiones, adecuados para sumas, promedios y resúmenes de percentiles. Utilice la métrica para calcular el volumen total de caída en un período de informe y comparar la calidad de representación de fotogramas en contenido, redes o reproductores.

## Cálculo de esta métrica

El reproductor actualiza el valor `droppedFrames` del objeto QoE a medida que se acumulan las gotas. El servidor informa del valor más reciente en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.droppedFrameCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

Para los informes booleanos de nivel de sesión (independientemente de si se descartaron fotogramas), use [Flujos afectados por fotogramas rechazados](dropped-frame-impacted-streams.md).
