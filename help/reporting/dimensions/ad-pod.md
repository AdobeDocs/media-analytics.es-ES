---
title: Pod de anuncios
description: Informa de cada pausa publicitaria única, introducida por un ID de pod generado automáticamente.
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
source-wordcount: '197'
ht-degree: 8%
---

# Pod de anuncios

La dimensión **pod de anuncios** informa de cada pausa de anuncio única, escrita por un ID de pod generado automáticamente. Cada anuncio de una sesión pertenece a un pod de anuncios principal y el pod agrupa varios anuncios reproducidos de forma consecutiva. Utilice la dimensión para dividir la participación por pausa publicitaria y como clave de unión para las clasificaciones [Pod name](pod-name.md) y [Pod position](pod-position.md).

## Cómo se rellena esta dimensión

SDK genera automáticamente el ID del pod de anuncios cuando se activa un evento [ad break start](/help/implementation/events/ads/ad-break-start.md). Las implementaciones de API directas lo construyen a partir del índice de interrupción y la hora de inicio, o proporcionan un ID de pod personalizado.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.pod` cuando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Fuentes de datos | `videoadpod`, `post_videoadpod` |
| Audience Manager | N/A |

## Elementos de dimensión

Cada elemento es un ID único de pod de anuncios. El identificador es opaco (normalmente un hash de ID de sesión, ID de contenido e índice de interrupción) y resulta más útil como clave de agrupación cuando se combina con [Nombre de secuencia](pod-name.md) para la etiqueta descriptiva.
