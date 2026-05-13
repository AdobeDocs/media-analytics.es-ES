---
title: ID de campaña
description: Informa de la campaña a la que pertenece cada anuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# ID de campaña

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **ID de campaña**. Consulte [ID de campaña](/help/implementation/variables/ads/campaign-id.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **ID de campaña** indica la campaña de publicidad a la que pertenece cada creativo de publicidad. Utilice la dimensión para resumir la participación en varios creativos que comparten una campaña.

## Cómo se rellena esta dimensión

El reproductor establece el ID de campaña en cada evento de `media.adStart`.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.campaign` cuando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videocampaign, post_videocampaign` |

## Elementos de dimensión

Cada elemento es el valor literal de campaña registrado en `media.adStart`.
