---
title: Duración del anuncio
description: Notifica la duración en segundos de cada anuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 5%

---


# Duración del anuncio

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Duración del anuncio**. Consulte [Duración del anuncio](/help/implementation/variables/ads/ad-length.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Longitud del anuncio** indica la duración en segundos de cada anuncio.

## Cómo se rellena esta dimensión

El reproductor establece la longitud del anuncio en cada evento de `media.adStart`.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.length` cuando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videoadlength, post_videoadlength` |

En Adobe Analytics, esta dimensión aparece de dos maneras: como **Longitud del anuncio (variable)** (recopilado directamente de `a.media.ad.length`) y como **Longitud del anuncio** (una clasificación derivada de la dimensión [Ad](ad.md)). Si usa la clasificación, usted es responsable de rellenar y mantener sus valores mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). El uso de **Duración del anuncio (variable)** no requiere mantenimiento de clasificación, pero se pierde la relación garantizada de 1:1 entre la duración del anuncio y la dimensión principal [Anuncio](ad.md). Utilice el componente que admita mejor el flujo de trabajo de implementación.

## Elementos de dimensión

Cada elemento es el valor literal de longitud de anuncio, en segundos, registrado en `media.adStart`.
