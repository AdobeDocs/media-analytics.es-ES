---
title: ID del sitio
description: Informa del identificador del sitio del anuncio de cada anuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 9%

---


# ID del sitio

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **ID del sitio**. Consulte [Id. de sitio](/help/implementation/variables/ads/site-id.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **ID del sitio** indica el identificador del sitio de publicidad (normalmente un ID de su plataforma de servidor de publicidad). Utilice la dimensión para desglosar la participación por sitio de ubicación de publicidad.

## Cómo se rellena esta dimensión

El reproductor establece el ID del sitio en cada evento de `media.adStart`.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.ad.site` a un eVar. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.ad.site`) |

## Elementos de dimensión

Cada elemento es el valor literal de id. de sitio registrado en `media.adStart`.
