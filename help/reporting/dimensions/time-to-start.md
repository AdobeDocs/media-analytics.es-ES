---
title: Tiempo para el inicio (dimensión)
description: Informa del tiempo transcurrido antes de que se represente el primer fotograma.
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
source-wordcount: '190'
ht-degree: 7%
---

# Tiempo para el inicio (dimensión)

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión **Tiempo para el inicio**. Adobe Analytics rellena automáticamente un par [Tiempo para el inicio (métrica)](/help/reporting/metrics/time-to-start.md) desde la misma variable de datos de contexto `a.media.qoe.timeToStart`. Customer Journey Analytics expone un único campo `xdm.mediaReporting.qoeDataDetails.timeToStart` que puede usar como dimensión o como métrica. Consulte [Tiempo para el inicio](/help/implementation/variables/quality/time-to-start.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Tiempo para el inicio** indica el tiempo transcurrido entre el inicio de la sesión y la primera representación del fotograma. Utilice la dimensión para desglosar la participación por bloque de tiempo de inicio. Adobe almacena el valor en segundos y lo convierte en el momento de la ingesta a partir de los milisegundos que informa el reproductor.

## Cómo se rellena esta dimensión

El reproductor establece `timeToStart` en el objeto QoE antes de que se active el inicio de sesión. El servidor informa del valor en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.timeToStart` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoetimetostartevar`, `post_videoqoetimetostartevar` |
| Audience Manager | `c_contextdata.a.media.qoe.timeToStart` |

## Elementos de dimensión

Cada elemento es el valor literal del tiempo de inicio registrado en la llamada de cierre.
