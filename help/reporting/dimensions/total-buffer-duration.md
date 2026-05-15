---
title: Duración total del búfer (dimensión)
description: Informa de los segundos acumulados empleados en el almacenamiento en búfer por sesión.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# Duración total del búfer (dimensión)

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión **Duración total del búfer**. Adobe Analytics rellena automáticamente un [Duración total del búfer (métrica)](/help/reporting/metrics/total-buffer-duration.md) emparejado desde la misma variable de datos de contexto `a.media.qoe.bufferTime`. Customer Journey Analytics expone un único campo `mediaReporting.qoeDataDetails.bufferTime` que puede usar como dimensión o como métrica.*

>[!ENDSHADEBOX]

La dimensión **Duración total del búfer** indica el tiempo acumulado, en segundos, que el reproductor ha pasado en estado de búfer durante una sesión. Utilice la dimensión para desglosar la participación según el valor exacto de duración del búfer.

## Cómo se rellena esta dimensión

El servidor multimedia suma la duración de cada intervalo de búfer (desde [inicio del búfer](/help/implementation/events/playback/buffer-start.md) hasta el siguiente cambio de estado). El valor se comunica en la llamada de cierre. Analysis Workspace muestra el valor como `HH:MM:SS`; fuentes de datos, Data Warehouse y API de informes muestran el valor en segundos.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bufferTime` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoebuffertimeevar`, `post_videoqoebuffertimeevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |

## Elementos de dimensión

Cada elemento es el valor de duración literal, en segundos, registrado en la llamada de cierre.
