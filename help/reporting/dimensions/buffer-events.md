---
title: Eventos de búfer (dimensión)
description: Notifica el recuento de eventos de almacenamiento en búfer por sesión.
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
source-wordcount: '175'
ht-degree: 8%
---

# Eventos de búfer (dimensión)

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión **Eventos de búfer**. Adobe Analytics rellena automáticamente [eventos de búfer (métrica)](/help/reporting/metrics/buffer-events.md) emparejados desde la misma variable de datos de contexto `a.media.qoe.bufferCount`. Customer Journey Analytics expone un único campo `xdm.mediaReporting.qoeDataDetails.bufferCount` que puede usar como dimensión o como métrica.*

>[!ENDSHADEBOX]

La dimensión **Eventos de búfer** indica el recuento de eventos de almacenamiento en búfer que se produjeron durante una sesión. Utilice la dimensión para desglosar la participación según el recuento exacto de búferes.

## Cómo se rellena esta dimensión

El servidor multimedia incrementa el recuento cada vez que el reproductor entra en un estado `buffer`. El valor se comunica en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.bufferCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## Elementos de dimensión

Cada elemento es el valor literal de recuento de búfer registrado en la llamada de cierre. Para los informes booleanos de nivel de sesión (independientemente de si la sesión experimentó almacenamiento en búfer), use [Flujos afectados por el búfer](/help/reporting/metrics/buffer-impacted-streams.md).
