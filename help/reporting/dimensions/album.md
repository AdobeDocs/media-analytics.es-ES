---
title: Álbum
description: Informa del álbum al que pertenece la pista de audio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 8%

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
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.album` cuando [[!UICONTROL Metadatos de audio]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoaudioalbum` |

## Elementos de dimensión

Cada elemento es el título literal del álbum registrado al inicio de la sesión. Dos álbumes con el mismo título de diferentes artistas se contraen en un solo elemento de línea. Emparejar con la dimensión [Artista](artist.md) para desambiguar.
