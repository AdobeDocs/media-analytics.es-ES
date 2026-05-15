---
title: Nombre del anuncio
description: Informa del título legible en lenguaje natural de cada anuncio.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 6%

---


# Nombre del anuncio

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Nombre del anuncio**. Consulte [Nombre del anuncio](/help/implementation/variables/ads/ad-name.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Nombre del anuncio** indica el título legible en lenguaje natural de cada anuncio.

## Cómo se rellena esta dimensión

El nombre del anuncio lo establece el reproductor en cada evento de [inicio del anuncio](/help/implementation/events/ads/ad-start.md).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.friendlyName` cuando [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videoadname`, `post_videoadname` |
| Audience Manager | `c_contextdata.a.media.ad.friendlyName` |

En Adobe Analytics, esta dimensión aparece de dos maneras: como **Nombre del anuncio (variable)** (recopilado directamente de `a.media.ad.friendlyName`) y como **Nombre del anuncio** (una clasificación derivada de la dimensión [Ad](ad.md)). Si usa la clasificación, usted es responsable de rellenar y mantener sus valores mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). El uso de **Ad name (variable)** no requiere mantenimiento de clasificación, pero se pierde la relación garantizada de 1:1 entre el nombre del anuncio y la dimensión principal [Ad](ad.md). Utilice el componente que admita mejor el flujo de trabajo de implementación.

## Elementos de dimensión

Cada elemento es el título literal del anuncio registrado en [inicio del anuncio](/help/implementation/events/ads/ad-start.md) (por ejemplo, `"Ford F-150"`).
