---
title: ID de colocación
description: Informa del identificador de ubicación de cada anuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 9%

---


# ID de colocación

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **ID de ubicación**. Consulte [ID. de ubicación](/help/implementation/variables/ads/placement-id.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **ID de ubicación** indica el identificador de ubicación del anuncio (normalmente una ranura o zona definida en la plataforma del servidor de publicidad). Utilice la dimensión para comparar la participación y la finalización en las ranuras de ubicación.

## Cómo se rellena esta dimensión

El reproductor establece el ID de ubicación en cada evento de `media.adStart`.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.ad.placement` a un eVar. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.ad.placement`) |

## Elementos de dimensión

Cada elemento es el valor de ubicación literal registrado en `media.adStart`.
