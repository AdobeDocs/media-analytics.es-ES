---
title: Anunciante
description: Informa de la empresa o marca que aparece en cada anuncio.
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
source-wordcount: '117'
ht-degree: 13%
---

# Anunciante

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Anunciante**. Consulte [Anunciante](/help/implementation/variables/ads/advertiser.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Anunciante** indica la compañía o marca que aparece en cada anuncio (por ejemplo, `"Ford"` o `"Coca-Cola"`). Utilice la dimensión para desglosar la participación y la finalización por parte del anunciante.

## Cómo se rellena esta dimensión

El reproductor establece el anunciante en cada [evento de inicio de publicidad](/help/implementation/events/ads/ad-start.md).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.advertiser` cuando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videoadvertiser`, `post_videoadvertiser` |
| Audience Manager | `c_contextdata.a.media.ad.advertiser` |

## Elementos de dimensión

Cada elemento es el nombre literal del anunciante registrado en [inicio del anuncio](/help/implementation/events/ads/ad-start.md).
