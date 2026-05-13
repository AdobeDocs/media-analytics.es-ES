---
title: Artista
description: Informa sobre el contenido de audio del artista intérprete o ejecutante.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 9%

---


# Artista

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Artista**. Consulte [Artista](/help/implementation/variables/standard-metadata/artist.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Artista** indica el artista intérprete para el contenido de audio (por ejemplo, `"Crested Larks"`). Utilícelo para generar participación en catálogos de música o podcast por intérprete.

## Cómo se rellena esta dimensión

El reproductor establece el artista al inicio de la sesión para el contenido de audio.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.artist` cuando [[!UICONTROL Metadatos de audio]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoaudioartist` |

## Elementos de dimensión

Cada elemento es el nombre literal del intérprete registrado al inicio de la sesión. Utilice un nombre canónico estable por artista para que los datos no se fragmenten en las variantes de formato.
