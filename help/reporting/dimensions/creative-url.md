---
title: URL del anuncio
description: Informa de la URL del recurso de cada creativo de publicidad.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 9%

---


# URL del anuncio

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **URL de Creative**. Consulte [URL de Creative](/help/implementation/variables/ads/creative-url.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **URL de Creative** indica la URL de recurso de cada creativo de publicidad. Utilice la dimensión cuando la propia URL sea significativa para el análisis (por ejemplo, para distinguir rutas CDN o versiones creativas).

## Cómo se rellena esta dimensión

El reproductor establece la URL de Creative en cada evento de `media.adStart`.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.ad.creativeURL` a un eVar. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.ad.creativeURL`) |

## Elementos de dimensión

Cada elemento es la cadena URL literal registrada en `media.adStart`.
