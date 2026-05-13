---
title: Nombre del reproductor del anuncio
description: Informa sobre qué reproductor procesó cada anuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---


# Nombre del reproductor del anuncio

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Nombre del reproductor del anuncio**. Consulte [Nombre del reproductor del anuncio](/help/implementation/variables/ads/ad-player-name.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Nombre del reproductor del anuncio** indica qué reproductor procesó cada anuncio (por ejemplo, `"Freewheel"`, `"Google IMA"`). El reproductor de anuncios puede diferir del reproductor de contenido principal cuando un servicio de inserción de anuncios del lado del servidor vincula los anuncios.

## Cómo se rellena esta dimensión

El nombre del reproductor de anuncios lo establece el reproductor en cada evento de `media.adStart`.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.playerName` cuando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videoadplayername, post_videoadplayername` |

## Elementos de dimensión

Cada elemento es el nombre literal del reproductor de anuncios registrado en `media.adStart`.
