---
title: ID de colocación
description: Informa del identificador de ubicación de cada anuncio.
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
source-wordcount: '151'
ht-degree: 10%
---

# ID de colocación

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **ID de ubicación**. Consulte [ID. de ubicación](/help/implementation/variables/ads/placement-id.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **ID de ubicación** indica el identificador de ubicación del anuncio (normalmente una ranura o zona definida en la plataforma del servidor de publicidad). Utilice la dimensión para comparar la participación y la finalización en las ranuras de ubicación.

## Cómo se rellena esta dimensión

El reproductor establece el ID de ubicación en cada [evento de inicio de anuncio](/help/implementation/events/ads/ad-start.md).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.ad.placement` a un eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.ad.placement`) |
| Audience Manager | `c_contextdata.a.media.ad.placement` |

## Elementos de dimensión

Cada elemento es el valor de ubicación literal registrado en [inicio de publicidad](/help/implementation/events/ads/ad-start.md).
