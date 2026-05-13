---
title: Cambios de velocidad de bits (dimensión)
description: Informa del recuento de eventos de cambio de velocidad de bits por sesión.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 5%

---


# Cambios de velocidad de bits (dimensión)

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión **Cambios de velocidad de bits**. Adobe Analytics rellena automáticamente un par de [cambios de velocidad de bits (métrica)](/help/reporting/metrics/bitrate-changes.md) de la misma variable de datos de contexto `a.media.qoe.bitrateChangeCount`. Customer Journey Analytics expone un único campo `mediaReporting.qoeDataDetails.bitrateChangeCount` que puede usar como dimensión o como métrica. Consulte [Cambio de velocidad de bits](/help/implementation/variables/quality/bitrate-change.md) para saber cómo activar eventos de cambio de velocidad de bits.*

>[!ENDSHADEBOX]

La dimensión **Cambios de velocidad de bits** indica el recuento de eventos de cambio de velocidad de bits que se produjeron durante una sesión. Utilice la dimensión para dividir la participación y la calidad por el valor exacto del recuento de cambios (por ejemplo, &quot;sesiones con 3 cambios de velocidad de bits frente a sesiones con 0&quot;).

## Cómo se rellena esta dimensión

El servidor multimedia incrementa el recuento de cada evento de `media.bitrateChange` recibido durante la sesión. El valor se comunica en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bitrateChangeCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoebitratechangecountevar, post_videoqoebitratechangecountevar` |

## Elementos de dimensión

Cada elemento es el valor literal de recuento de cambios registrado en la llamada de cierre. Para los informes booleanos de nivel de sesión (independientemente de si la sesión experimentó algún cambio en la velocidad de bits), use [Flujos afectados por el cambio en la velocidad de bits](/help/reporting/metrics/bitrate-change-impacted-streams.md).
