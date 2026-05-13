---
title: Fotogramas perdidos (dimensión)
description: Informa del recuento acumulado de fotogramas perdidos por sesión.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 5%

---


# Fotogramas perdidos (dimensión)

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión **fotogramas perdidos**. Adobe Analytics rellena automáticamente un par de [fotogramas perdidos (métrica)](/help/reporting/metrics/dropped-frames.md) desde la misma variable de datos de contexto `a.media.qoe.droppedFrameCount`. Customer Journey Analytics expone un único campo `mediaReporting.qoeDataDetails.droppedFrames` que puede usar como dimensión o como métrica. Consulte [Fotogramas perdidos](/help/implementation/variables/quality/dropped-frames.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **fotogramas perdidos** indica el número acumulado de fotogramas perdidos durante una sesión. Utilice la dimensión para desglosar la participación según el recuento de bajas exacto.

## Cómo se rellena esta dimensión

El reproductor actualiza el valor `droppedFrames` del objeto QoE a medida que acumula caídas. El servidor informa del valor más reciente en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.droppedFrameCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoedroppedframecountevar, post_videoqoedroppedframecountevar` |

## Elementos de dimensión

Cada elemento es el valor literal de recuento desplegable registrado en la llamada de cierre. Para los informes booleanos de nivel de sesión (independientemente de si se descartaron fotogramas), use [Flujos afectados por fotogramas rechazados](/help/reporting/metrics/dropped-frame-impacted-streams.md).
