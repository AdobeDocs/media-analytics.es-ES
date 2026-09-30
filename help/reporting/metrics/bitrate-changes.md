---
title: Cambios de velocidad de bits (métrica)
description: Cuenta los eventos de cambio de velocidad de bits para sumas y promedios entre sesiones.
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
source-wordcount: '208'
ht-degree: 7%
---

# Cambios de velocidad de bits (métrica)

>[!BEGINSHADEBOX]

*Esta página cubre la métrica **Cambios de velocidad de bits**. Adobe Analytics rellena automáticamente un par de [cambios de velocidad de bits (dimensión)](/help/reporting/dimensions/bitrate-changes.md) desde la misma variable de datos de contexto `a.media.qoe.bitrateChangeCount`. Customer Journey Analytics expone un único campo `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` que puede usar como dimensión o como métrica. Consulte [Cambio de velocidad de bits](/help/implementation/variables/quality/bitrate-change.md) para saber cómo activar eventos de cambio de velocidad de bits.*

>[!ENDSHADEBOX]

La métrica **Cambios de velocidad de bits** cuenta eventos de cambios en la velocidad de bits entre sesiones, adecuada para sumas, promedios y acumulaciones de percentiles. Utilice la métrica para calcular el volumen total de cambios en la velocidad de bits en un período de informe y comparar la estabilidad de la velocidad de bits en contenido, redes o reproductores.

## Cálculo de esta métrica

El servidor multimedia incrementa el recuento en cada [cambio de velocidad de bits](/help/implementation/events/playback/bitrate-change.md) evento recibido durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bitrateChangeCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

Para los informes booleanos de nivel de sesión (independientemente de si la sesión experimentó algún cambio en la velocidad de bits), use [Flujos afectados por el cambio en la velocidad de bits](bitrate-change-impacted-streams.md).
