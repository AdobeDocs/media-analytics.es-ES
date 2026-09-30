---
title: Errores
description: Informa del recuento de eventos de error por sesión.
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
source-wordcount: '235'
ht-degree: 6%
---

# Errores

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión **Errores**. Adobe Analytics rellena automáticamente una métrica emparejada de [eventos de error](/help/reporting/metrics/error-events.md) desde la misma variable de datos de contexto `a.media.qoe.errorCount`. Customer Journey Analytics expone un único campo `xdm.mediaReporting.qoeDataDetails.errorCount` que puede usar como dimensión o como métrica.*

>[!ENDSHADEBOX]

La dimensión **Errores** indica el recuento de eventos de error recibidos durante una sesión. Utilice la dimensión para desglosar la participación según el recuento de errores exacto.

## Cómo se rellena esta dimensión

El backend de medios aumenta el recuento de cada error notificado por el reproductor. El valor se comunica en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.errorCount` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoeerrorcountevar`, `post_videoqoeerrorcountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

## Elementos de dimensión

Cada elemento es el valor literal de recuento de errores notificado en la llamada de cierre. Para los informes booleanos de nivel de sesión (si se produjo algún error), use [Flujos afectados por errores](/help/reporting/metrics/error-impacted-streams.md). Para identificadores de error únicos, usa [ID de error externo](external-error-ids.md) e [ID de error del reproductor SDK](player-sdk-error-ids.md).

>[!NOTE]
>
>Si utiliza la versión heredada de Heartbeat para SDK (Media SDK 1.5.x-2.x), los ID de error generados internamente por SDK se recopilan automáticamente en la clave de datos de contexto `a.media.qoe.mediaSdkErrors` y se puede acceder a ellos en Adobe Analytics mediante una regla de procesamiento personalizada. El rasgo de Audience Manager es `c_contextdata.a.media.qoe.mediaSdkErrors`. Este campo no es aplicable a las implementaciones de la API de Media Collection o de la API de Media Edge.
