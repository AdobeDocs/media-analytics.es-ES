---
title: Tiempo para el inicio (dimensión)
description: Informa del tiempo transcurrido antes de que se represente el primer fotograma.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

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
