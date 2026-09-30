---
title: Posición del anuncio en la secuencia
description: Informa de la posición indexada cero de cada anuncio dentro de su pausa para anuncios principal.
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
source-wordcount: '156'
ht-degree: 8%
---

# Posición del anuncio en la secuencia

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión del informe **Anuncio en la posición del pod**. Consulte [Posición del anuncio en el pod](/help/implementation/variables/ads/ad-in-pod-position.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Posición del anuncio** indica la posición indizada cero de cada anuncio dentro de su pausa para anuncios principal. El primer anuncio de un pod es `0`, el segundo es `1`, etc. Utilice la dimensión para comparar la participación y la finalización por posición dentro de una pausa publicitaria.

## Cómo se rellena esta dimensión

El reproductor establece la posición del pod de anuncios en cada evento de [inicio del anuncio](/help/implementation/events/ads/ad-start.md).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.podPosition` cuando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videoadinpod`, `post_videoadinpod` |
| Audience Manager | `c_contextdata.a.media.ad.podPosition` |

## Elementos de dimensión

Cada elemento es el valor de posición entero (`0`, `1`, `2`, ...) se informó sobre [inicio del anuncio](/help/implementation/events/ads/ad-start.md).
