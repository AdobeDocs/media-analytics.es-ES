---
title: Fotogramas perdidos (dimensión)
description: Informa del recuento acumulado de fotogramas perdidos por sesión.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 7%
---

# Fotogramas perdidos (dimensión)

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión **fotogramas perdidos**. Adobe Analytics rellena automáticamente un par de [fotogramas perdidos (métrica)](/help/reporting/metrics/dropped-frames.md) desde la misma variable de datos de contexto `a.media.qoe.droppedFrameCount`. Customer Journey Analytics expone un único campo `xdm.mediaReporting.qoeDataDetails.droppedFrames` que puede usar como dimensión o como métrica. Consulte [Fotogramas perdidos](/help/implementation/variables/quality/dropped-frames.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **fotogramas perdidos** indica el número acumulado de fotogramas perdidos durante una sesión. Utilice la dimensión para desglosar la participación según el recuento de bajas exacto.

## Cómo se rellena esta dimensión

El reproductor actualiza el valor `droppedFrames` del objeto QoE a medida que acumula caídas. El servidor informa del valor más reciente en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.droppedFrameCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoedroppedframecountevar`, `post_videoqoedroppedframecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

## Elementos de dimensión

Cada elemento es el valor literal de recuento desplegable registrado en la llamada de cierre. Para los informes booleanos de nivel de sesión (independientemente de si se descartaron fotogramas), use [Flujos afectados por fotogramas rechazados](/help/reporting/metrics/dropped-frame-impacted-streams.md).
