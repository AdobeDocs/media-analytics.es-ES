---
title: Publicidad
description: Informa de cada anuncio único reproducido, marcado por el ID de anuncio.
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
source-wordcount: '188'
ht-degree: 8%
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
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.name` cuando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. Persiste durante la visita. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videoad`, `post_videoad` |
| Audience Manager | `c_contextdata.a.media.ad.name` |

>[!IMPORTANT]
>
>Se requiere el ID del anuncio. Si no se configura o está vacío, el anuncio se elimina de la creación de informes de anuncios de medios de streaming.

## Elementos de dimensión

Cada elemento es un ID de anuncio único registrado en [inicio del anuncio](/help/implementation/events/ads/ad-start.md). Utilice un identificador estable por creativo para que el mismo anuncio se reúna en un solo elemento de línea entre sesiones.
