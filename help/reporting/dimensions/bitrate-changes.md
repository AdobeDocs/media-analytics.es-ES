---
title: Cambios de velocidad de bits (dimensión)
description: Informa del recuento de eventos de cambio de velocidad de bits por sesión.
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
source-wordcount: '205'
ht-degree: 6%
---

# Cambios de velocidad de bits (dimensión)

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión **Cambios de velocidad de bits**. Adobe Analytics rellena automáticamente un par de [cambios de velocidad de bits (métrica)](/help/reporting/metrics/bitrate-changes.md) de la misma variable de datos de contexto `a.media.qoe.bitrateChangeCount`. Customer Journey Analytics expone un único campo `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` que puede usar como dimensión o como métrica. Consulte [Cambio de velocidad de bits](/help/implementation/variables/quality/bitrate-change.md) para saber cómo activar eventos de cambio de velocidad de bits.*

>[!ENDSHADEBOX]

La dimensión **Cambios de velocidad de bits** indica el recuento de eventos de cambio de velocidad de bits que se produjeron durante una sesión. Utilice la dimensión para dividir la participación y la calidad por el valor exacto del recuento de cambios (por ejemplo, &quot;sesiones con 3 cambios de velocidad de bits frente a sesiones con 0&quot;).

## Cómo se rellena esta dimensión

El servidor multimedia incrementa el recuento en cada [cambio de velocidad de bits](/help/implementation/events/playback/bitrate-change.md) evento recibido durante la sesión. El valor se comunica en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bitrateChangeCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoebitratechangecountevar`, `post_videoqoebitratechangecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

## Elementos de dimensión

Cada elemento es el valor literal de recuento de cambios registrado en la llamada de cierre. Para los informes booleanos de nivel de sesión (independientemente de si la sesión experimentó algún cambio en la velocidad de bits), use [Flujos afectados por el cambio en la velocidad de bits](/help/reporting/metrics/bitrate-change-impacted-streams.md).
