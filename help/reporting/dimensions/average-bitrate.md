---
title: Velocidad de bits media (dimensión)
description: Informa de la velocidad de bits media agrupada de cada sesión en intervalos de 100 kbps.
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
source-wordcount: '170'
ht-degree: 8%
---

# Velocidad de bits media (dimensión)

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión **Velocidad de bits media**, que indica la velocidad de bits agrupada de cada sesión. Consulte [Velocidad de bits promedio (métrica)](/help/reporting/metrics/average-bitrate.md) para la métrica promedio ponderado sin procesar. Consulte [Velocidad de bits](/help/implementation/variables/quality/bitrate.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Velocidad de bits promedio** indica la velocidad de bits de reproducción promedio por sesión, agrupada en intervalos de 100 kbps. El servidor calcula el valor como un promedio ponderado de todos los valores de velocidad de bits en la sesión y, a continuación, lo asigna a un bloque. Utilice la dimensión para desglosar la participación y la calidad por nivel de velocidad de bits.

## Cómo se rellena esta dimensión

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bitrateAverageBucket` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoebitrateaverageevar`, `post_videoqoebitrateaverageevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverageBucket` |

## Elementos de dimensión

Cada elemento es una etiqueta de bloque de velocidad de bits (por ejemplo, `800-899`, `3200-3299`). Use [Velocidad de bits promedio (métrica)](/help/reporting/metrics/average-bitrate.md) para un valor promedio ponderado sin procesar en lugar de una dimensión agrupada.
