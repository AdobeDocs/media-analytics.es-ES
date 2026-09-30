---
title: Nombre del anuncio
description: Informa del título legible en lenguaje natural de cada anuncio.
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
source-wordcount: '194'
ht-degree: 7%
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
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.ad.friendlyName` cuando [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos | `videoadname`, `post_videoadname` |
| Audience Manager | `c_contextdata.a.media.ad.friendlyName` |

En Adobe Analytics, esta dimensión aparece de dos maneras: como **Nombre del anuncio (variable)** (recopilado directamente de `a.media.ad.friendlyName`) y como **Nombre del anuncio** (una clasificación derivada de la dimensión [Ad](ad.md)). Si usa la clasificación, usted es responsable de rellenar y mantener sus valores mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). El uso de **Ad name (variable)** no requiere mantenimiento de clasificación, pero se pierde la relación 1:1 garantizada entre el nombre del anuncio y la dimensión principal [Ad](ad.md). Utilice el componente que admita mejor el flujo de trabajo de implementación.

## Elementos de dimensión

Cada elemento es el título literal del anuncio registrado en [inicio del anuncio](/help/implementation/events/ads/ad-start.md) (por ejemplo, `"Ford F-150"`).
