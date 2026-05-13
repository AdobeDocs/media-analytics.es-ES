---
title: Publicidad
description: Informa de cada anuncio único reproducido, marcado por el ID de anuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 6%

---


# Publicidad

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Ad**. Consulte [ID de anuncio](/help/implementation/variables/ads/ad-id.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Ad** indica cada anuncio único reproducido, marcado por el ID de anuncio establecido en `media.adStart`. La dimensión es el desglose principal para los informes de publicidad y la clave de unión para las clasificaciones de nivel de publicidad como el nombre del anuncio, la duración del anuncio y el ID de Creative.

## Cómo se rellena esta dimensión

El reproductor establece el anuncio en cada evento `media.adStart` como identificador estable para el anuncio.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.name` cuando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. Persiste durante la visita. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videoad, post_videoad` |

>[!IMPORTANT]
>
>Se requiere el ID del anuncio. Si no se configura o está vacío, el anuncio se elimina de la creación de informes de anuncios de medios de streaming.

## Elementos de dimensión

Cada elemento es un identificador de anuncio único registrado en `media.adStart`. Utilice un identificador estable por creativo para que el mismo anuncio se reúna en un solo elemento de línea entre sesiones.
