---
title: Posición del anuncio en la secuencia
description: Informa de la posición indexada cero de cada anuncio dentro de su pausa para anuncios principal.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 6%

---


# Posición del anuncio en la secuencia

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión del informe **Anuncio en la posición del pod**. Consulte [Posición del anuncio en el pod](/help/implementation/variables/ads/ad-in-pod-position.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Posición del anuncio** indica la posición indizada cero de cada anuncio dentro de su pausa para anuncios principal. El primer anuncio de un pod es `0`, el segundo es `1`, etc. Utilice la dimensión para comparar la participación y la finalización por posición dentro de una pausa publicitaria.

## Cómo se rellena esta dimensión

El reproductor establece la posición del pod en cada evento de `media.adStart`.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.podPosition` cuando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videoadinpod, post_videoadinpod` |

## Elementos de dimensión

Cada elemento es el valor de posición entero (`0`, `1`, `2`, ...) se informó sobre `media.adStart`.
