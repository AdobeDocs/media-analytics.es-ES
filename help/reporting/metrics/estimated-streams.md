---
title: Flujos estimados
description: Aproxima el número de transmisiones de audio o vídeo por sesión.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 10%

---


# Flujos estimados

La métrica **Flujos estimados** se aproxima al número de flujos de audio o vídeo por sesión, contándose un flujo por cada 30 minutos de reproducción total. Está pensado para acuerdos de distribución de contenido y alcanza aproximaciones en las que cada bloque de consumo de 30 minutos cuenta como un &quot;flujo&quot; independiente.

## Cálculo de esta métrica

El servidor multimedia calcula esta métrica como `FLOOR(totalTimePlayed / 1800) + 1`, donde `totalTimePlayed` es [tiempo invertido en contenido](media-time-spent.md) en segundos. La métrica se recoge en la llamada de cierre.

| Tiempo invertido en contenido | Flujos estimados |
| --- | --- |
| 0-29 min | 1 |
| 30-59 min | 2 |
| 60-89 min | 3 |
| Más de 90 min | 4+ |

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.estimatedStreams` a un evento personalizado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.estimatedStreams`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (el evento personalizado al que la regla de procesamiento asigna `a.media.estimatedStreams`; consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/es/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.estimatedStreams` |
