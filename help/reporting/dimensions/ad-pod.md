---
title: Pod de anuncios
description: Informa de cada pausa publicitaria única, introducida por un ID de pod generado automáticamente.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# Pod de anuncios

La dimensión **pod de anuncios** informa de cada pausa de anuncio única, escrita por un ID de pod generado automáticamente. Cada anuncio de una sesión pertenece a un pod de anuncios principal y el pod agrupa varios anuncios reproducidos de forma consecutiva. Utilice la dimensión para dividir la participación por pausa publicitaria y como clave de unión para las clasificaciones [Pod name](pod-name.md) y [Pod position](pod-position.md).

## Cómo se rellena esta dimensión

SDK genera automáticamente el ID del pod de anuncios cuando se activa un evento [ad break start](/help/implementation/events/ads/ad-break-start.md). Las implementaciones de API directas lo construyen a partir del índice de interrupción y la hora de inicio, o proporcionan un ID de pod personalizado.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.pod` cuando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Fuentes de datos | `videoadpod`, `post_videoadpod` |
| Audience Manager | N/A |

## Elementos de dimensión

Cada elemento es un ID único de pod de anuncios. El identificador es opaco (normalmente un hash de ID de sesión, ID de contenido e índice de interrupción) y resulta más útil como clave de agrupación cuando se combina con [Nombre de secuencia](pod-name.md) para la etiqueta descriptiva.
