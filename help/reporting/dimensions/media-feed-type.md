---
title: Tipo de fuente de medios
description: Informa de la fuente de difusión (por ejemplo, East-HD u West-SD) cuando el mismo contenido se entrega a través de varias fuentes.
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
source-wordcount: '159'
ht-degree: 8%
---

# Tipo de fuente de medios

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Tipo de fuente de medios**. Consulte [Tipo de fuente de medios](/help/implementation/variables/standard-metadata/media-feed-type.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Tipo de fuente de medios** informa de la fuente de difusión de cada sesión (por ejemplo, `"East-HD"`, `"West-SD"` o `"4K"`). Utilícelo cuando el mismo contenido se entregue a través de varias fuentes regionales o de calidad y la participación deba comunicarse por fuente.

## Cómo se rellena esta dimensión

El reproductor establece el tipo de fuente de medios al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.feed` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## Elementos de dimensión

Cada elemento es el valor de fuente literal registrado al inicio de la sesión. Utilice un conjunto estable de identificadores de fuentes por división regional o de calidad.
