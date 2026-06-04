---
title: Eventos de búfer (dimensión)
description: Notifica el recuento de eventos de almacenamiento en búfer por sesión.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

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
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## Elementos de dimensión

Cada elemento es el valor literal de recuento de búfer registrado en la llamada de cierre. Para los informes booleanos de nivel de sesión (independientemente de si la sesión experimentó almacenamiento en búfer), use [Flujos afectados por el búfer](/help/reporting/metrics/buffer-impacted-streams.md).
