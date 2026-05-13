---
title: Fotogramas perdidos (métrica)
description: Informa de los fotogramas perdidos acumulados para sumas y promedios entre sesiones.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 6%

---


# Fotogramas perdidos (métrica)

>[!BEGINSHADEBOX]

*Esta página cubre la métrica **fotogramas perdidos**. Adobe Analytics rellena automáticamente un par de [fotogramas perdidos (dimensión)](/help/reporting/dimensions/dropped-frames.md) desde la misma variable de datos de contexto `a.media.qoe.droppedFrameCount`. Customer Journey Analytics expone un único campo `mediaReporting.qoeDataDetails.droppedFrames` que puede usar como dimensión o como métrica. Consulte [Fotogramas perdidos](/help/implementation/variables/quality/dropped-frames.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Fotogramas perdidos** indica fotogramas perdidos acumulados entre sesiones, adecuados para sumas, promedios y resúmenes de percentiles. Utilice la métrica para calcular el volumen total de caída en un período de informe y comparar la calidad de representación de fotogramas en contenido, redes o reproductores.

## Cálculo de esta métrica

El reproductor actualiza el valor `droppedFrames` del objeto QoE a medida que se acumulan las gotas. El servidor informa del valor más reciente en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.droppedFrameCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |

Para los informes booleanos de nivel de sesión (independientemente de si se descartaron fotogramas), use [Flujos afectados por fotogramas rechazados](dropped-frame-impacted-streams.md).
