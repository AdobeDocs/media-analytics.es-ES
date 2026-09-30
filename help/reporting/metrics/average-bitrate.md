---
title: Velocidad de bits media (métrica)
description: Informa de la velocidad de bits media ponderada sin procesar de cada sesión, en kbps.
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
source-wordcount: '175'
ht-degree: 8%
---

# Velocidad de bits media (métrica)

>[!BEGINSHADEBOX]

*Esta página cubre la métrica de evento **Velocidad de bits promedio**, que indica la velocidad de bits promedio ponderada sin procesar por sesión. Consulte [Velocidad de bits media (dimensión)](/help/reporting/dimensions/average-bitrate.md) para la dimensión agrupada. Consulte [Velocidad de bits](/help/implementation/variables/quality/bitrate.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La métrica **Velocidad de bits promedio** indica la velocidad de bits de reproducción media ponderada sin procesar, en kbps, para cada sesión. A diferencia de la [dimensión agrupada](/help/reporting/dimensions/average-bitrate.md), la métrica es un valor numérico continuo adecuado para sumas, promedios y acumulaciones de percentiles entre sesiones.

## Cálculo de esta métrica

El servidor de contenido calcula una media ponderada de todos los valores de velocidad de bits comunicados durante la sesión, ponderada por la duración en que cada velocidad de bits estaba activa. La métrica se recoge en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bitrateAverage` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateAverage`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `event_list`, `post_event_list` (consulte la búsqueda [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverage` |
