---
title: Nombre del reproductor del anuncio
description: Informa sobre qué reproductor procesó cada anuncio.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

---


# Nombre del reproductor del anuncio

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Nombre del reproductor del anuncio**. Consulte [Nombre del reproductor del anuncio](/help/implementation/variables/ads/ad-player-name.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Nombre del reproductor del anuncio** indica qué reproductor procesó cada anuncio (por ejemplo, `"Freewheel"`, `"Google IMA"`). El reproductor de anuncios puede diferir del reproductor de contenido principal cuando un servicio de inserción de anuncios del lado del servidor vincula los anuncios.

## Cómo se rellena esta dimensión

El reproductor establece el nombre del reproductor del anuncio en cada evento de [inicio del anuncio](/help/implementation/events/ads/ad-start.md).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.playerName` cuando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videoadplayername`, `post_videoadplayername` |
| Audience Manager | `c_contextdata.a.media.ad.playerName` |

## Elementos de dimensión

Cada elemento es el nombre literal del reproductor de anuncios registrado en [inicio del anuncio](/help/implementation/events/ads/ad-start.md).
