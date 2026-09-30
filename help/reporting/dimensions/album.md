---
title: Álbum
description: Informa del álbum al que pertenece la pista de audio.
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
source-wordcount: '136'
ht-degree: 10%
---

# Álbum

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Álbum**. Consulte [Álbum](/help/implementation/variables/standard-metadata/album.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Álbum** indica el álbum al que pertenece la pista de audio (por ejemplo, `"Pinegrove"`). Utilícelo para resumir la participación en todas las pistas del mismo álbum.

## Cómo se rellena esta dimensión

El reproductor establece el álbum al principio de la sesión para el contenido de audio.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.album` cuando [[!UICONTROL Metadatos de audio]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoaudioalbum` |
| Audience Manager | `c_contextdata.a.media.album` |

## Elementos de dimensión

Cada elemento es el título literal del álbum registrado al inicio de la sesión. Dos álbumes con el mismo título de diferentes artistas se contraen en un solo elemento de línea. Emparejar con la dimensión [Artista](artist.md) para desambiguar.
