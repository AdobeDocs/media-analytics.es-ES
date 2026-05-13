---
title: Tipo de fuente de medios
description: Informa de la fuente de difusión (por ejemplo, East-HD u West-SD) cuando el mismo contenido se entrega a través de varias fuentes.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 6%

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
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.feed` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videofeedtype, post_videofeedtype` |

## Elementos de dimensión

Cada elemento es el valor de fuente literal registrado al inicio de la sesión. Utilice un conjunto estable de identificadores de fuentes por división regional o de calidad.
