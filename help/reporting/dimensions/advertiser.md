---
title: Anunciante
description: Informa de la empresa o marca que aparece en cada anuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 11%

---


# Anunciante

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Anunciante**. Consulte [Anunciante](/help/implementation/variables/ads/advertiser.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Anunciante** indica la compañía o marca que aparece en cada anuncio (por ejemplo, `"Ford"` o `"Coca-Cola"`). Utilice la dimensión para desglosar la participación y la finalización por parte del anunciante.

## Cómo se rellena esta dimensión

El reproductor establece el anunciante en cada evento de `media.adStart`.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.advertiser` cuando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videoadvertiser, post_videoadvertiser` |

## Elementos de dimensión

Cada elemento es el nombre literal del anunciante registrado en `media.adStart`.
