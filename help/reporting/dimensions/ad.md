---
title: Publicidad
description: Informa de cada anuncio único reproducido, marcado por el ID de anuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 7%

---


# Publicidad

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Ad**. Consulte [ID de anuncio](/help/implementation/variables/ads/ad-id.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Ad** indica cada anuncio único reproducido, marcado por el ID de anuncio establecido en [inicio del anuncio](/help/implementation/events/ads/ad-start.md). La dimensión es el desglose principal para los informes de publicidad y la clave de unión para las clasificaciones de nivel de publicidad como el nombre del anuncio, la duración del anuncio y el ID de Creative.

## Cómo se rellena esta dimensión

El reproductor establece el anuncio en cada evento de [inicio del anuncio](/help/implementation/events/ads/ad-start.md) como identificador estable del anuncio.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.name` cuando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. Persiste durante la visita. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videoad`, `post_videoad` |
| Audience Manager | `c_contextdata.a.media.ad.name` |

>[!IMPORTANT]
>
>Se requiere el ID del anuncio. Si no se configura o está vacío, el anuncio se elimina de la creación de informes de anuncios de medios de streaming.

## Elementos de dimensión

Cada elemento es un ID de anuncio único registrado en [inicio del anuncio](/help/implementation/events/ads/ad-start.md). Utilice un identificador estable por creativo para que el mismo anuncio se reúna en un solo elemento de línea entre sesiones.
