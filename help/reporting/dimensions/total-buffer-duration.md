---
title: Duración total del búfer (dimensión)
description: Informa de los segundos acumulados empleados en el almacenamiento en búfer por sesión.
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
source-wordcount: '194'
ht-degree: 7%
---

# Duración total del búfer (dimensión)

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión **Duración total del búfer**. Adobe Analytics rellena automáticamente un [Duración total del búfer (métrica)](/help/reporting/metrics/total-buffer-duration.md) emparejado desde la misma variable de datos de contexto `a.media.qoe.bufferTime`. Customer Journey Analytics expone un único campo `xdm.mediaReporting.qoeDataDetails.bufferTime` que puede usar como dimensión o como métrica.*

>[!ENDSHADEBOX]

La dimensión **Duración total del búfer** indica el tiempo acumulado, en segundos, que el reproductor ha pasado en estado de búfer durante una sesión. Utilice la dimensión para desglosar la participación según el valor exacto de duración del búfer.

## Cómo se rellena esta dimensión

El servidor multimedia suma la duración de cada intervalo de búfer (desde [inicio del búfer](/help/implementation/events/playback/buffer-start.md) hasta el siguiente cambio de estado). El valor se comunica en la llamada de cierre. Analysis Workspace muestra el valor como `HH:MM:SS`; fuentes de datos, Data Warehouse y API de informes muestran el valor en segundos.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bufferTime` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoebuffertimeevar`, `post_videoqoebuffertimeevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |

## Elementos de dimensión

Cada elemento es el valor de duración literal, en segundos, registrado en la llamada de cierre.
