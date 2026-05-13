---
title: Eventos de error
description: Cuenta los eventos de error para las sumas y promedios entre sesiones.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 7%

---


# Eventos de error

>[!BEGINSHADEBOX]

*Esta página cubre la métrica **Eventos de error**. Adobe Analytics rellena automáticamente una dimensión emparejada de [errores](/help/reporting/dimensions/errors.md) desde la misma variable de datos de contexto `a.media.qoe.errorCount`. Customer Journey Analytics expone un único campo `mediaReporting.qoeDataDetails.errorCount` que puede usar como dimensión o como métrica.*

>[!ENDSHADEBOX]

La métrica **Eventos de error** cuenta los eventos de error en todas las sesiones, lo cual es adecuado para sumas, promedios y resúmenes de percentiles. Utilice la métrica para calcular el volumen total de errores en un período de informe y comparar las tasas de error entre contenido, redes o reproductores.

## Cálculo de esta métrica

El backend de medios aumenta el recuento de cada error notificado por el reproductor. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.errorCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |

Para los informes booleanos de nivel de sesión (si se produjo algún error), use [Flujos afectados por errores](error-impacted-streams.md).
