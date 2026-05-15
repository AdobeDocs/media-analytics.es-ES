---
title: Velocidad de bits media (dimensión)
description: Informa de la velocidad de bits media agrupada de cada sesión en intervalos de 100 kbps.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# Velocidad de bits media (dimensión)

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión **Velocidad de bits media**, que indica la velocidad de bits agrupada de cada sesión. Consulte [Velocidad de bits promedio (métrica)](/help/reporting/metrics/average-bitrate.md) para la métrica promedio ponderado sin procesar. Consulte [Velocidad de bits](/help/implementation/variables/quality/bitrate.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Velocidad de bits promedio** indica la velocidad de bits de reproducción promedio por sesión, agrupada en intervalos de 100 kbps. El servidor calcula el valor como un promedio ponderado de todos los valores de velocidad de bits en la sesión y, a continuación, lo asigna a un bloque. Utilice la dimensión para desglosar la participación y la calidad por nivel de velocidad de bits.

## Cómo se rellena esta dimensión

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bitrateAverageBucket` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoebitrateaverageevar`, `post_videoqoebitrateaverageevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverageBucket` |

## Elementos de dimensión

Cada elemento es una etiqueta de bloque de velocidad de bits (por ejemplo, `800-899`, `3200-3299`). Use [Velocidad de bits promedio (métrica)](/help/reporting/metrics/average-bitrate.md) para un valor promedio ponderado sin procesar en lugar de una dimensión agrupada.
