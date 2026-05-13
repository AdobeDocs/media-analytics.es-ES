---
title: Cambios de velocidad de bits (métrica)
description: Cuenta los eventos de cambio de velocidad de bits para sumas y promedios entre sesiones.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 6%

---


# Cambios de velocidad de bits (métrica)

>[!BEGINSHADEBOX]

*Esta página cubre la métrica **Cambios de velocidad de bits**. Adobe Analytics rellena automáticamente un par de [cambios de velocidad de bits (dimensión)](/help/reporting/dimensions/bitrate-changes.md) desde la misma variable de datos de contexto `a.media.qoe.bitrateChangeCount`. Customer Journey Analytics expone un único campo `mediaReporting.qoeDataDetails.bitrateChangeCount` que puede usar como dimensión o como métrica. Consulte [Cambio de velocidad de bits](/help/implementation/variables/quality/bitrate-change.md) para saber cómo activar eventos de cambio de velocidad de bits.*

>[!ENDSHADEBOX]

La métrica **Cambios de velocidad de bits** cuenta eventos de cambios en la velocidad de bits entre sesiones, adecuada para sumas, promedios y acumulaciones de percentiles. Utilice la métrica para calcular el volumen total de cambios en la velocidad de bits en un período de informe y comparar la estabilidad de la velocidad de bits en contenido, redes o reproductores.

## Cálculo de esta métrica

El servidor multimedia incrementa el recuento de cada evento de `media.bitrateChange` recibido durante la sesión. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bitrateChangeCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |

Para los informes booleanos de nivel de sesión (independientemente de si la sesión experimentó algún cambio en la velocidad de bits), use [Flujos afectados por el cambio en la velocidad de bits](bitrate-change-impacted-streams.md).
