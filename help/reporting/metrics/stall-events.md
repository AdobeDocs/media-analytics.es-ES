---
title: Eventos de detención
description: Cuenta los eventos de estancamiento para las sumas y los promedios entre sesiones.
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
source-wordcount: '203'
ht-degree: 7%
---

# Eventos de detención

La métrica **Eventos de detención** cuenta los eventos de detención en todas las sesiones, lo cual es adecuado para sumas, promedios y acumulaciones de percentiles. Utilice la métrica para calcular el volumen total de detención en un período de informe y comparar la estabilidad de detención en contenido, redes o reproductores.

En Customer Journey Analytics, `xdm.mediaReporting.qoeDataDetails.stallCount` se puede usar como métrica o como dimensión sin un componente de dimensión independiente.

## Cálculo de esta métrica

El back-end de medios aumenta el recuento cada vez que no se registra ningún movimiento del cabezal de reproducción en el contenido principal durante al menos tres eventos consecutivos. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.qoe.stallCount` a un evento personalizado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (el evento personalizado al que la regla de procesamiento asigna `a.media.qoe.stallCount`; consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stallCount` |

Para los informes booleanos de nivel de sesión (independientemente de si se produjo alguna detención), use [Flujos afectados por detención](stall-impacted-streams.md).
