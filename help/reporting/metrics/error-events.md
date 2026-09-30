---
title: Eventos de error
description: Cuenta los eventos de error para las sumas y promedios entre sesiones.
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
source-wordcount: '184'
ht-degree: 8%
---

# Eventos de error

>[!BEGINSHADEBOX]

*Esta página cubre la métrica **Eventos de error**. Adobe Analytics rellena automáticamente una dimensión emparejada de [errores](/help/reporting/dimensions/errors.md) desde la misma variable de datos de contexto `a.media.qoe.errorCount`. Customer Journey Analytics expone un único campo `xdm.mediaReporting.qoeDataDetails.errorCount` que puede usar como dimensión o como métrica.*

>[!ENDSHADEBOX]

La métrica **Eventos de error** cuenta los eventos de error en todas las sesiones, lo cual es adecuado para sumas, promedios y resúmenes de percentiles. Utilice la métrica para calcular el volumen total de errores en un período de informe y comparar las tasas de error entre contenido, redes o reproductores.

## Cálculo de esta métrica

El backend de medios aumenta el recuento de cada error notificado por el reproductor. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.errorCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

Para los informes booleanos de nivel de sesión (si se produjo algún error), use [Flujos afectados por errores](error-impacted-streams.md).
