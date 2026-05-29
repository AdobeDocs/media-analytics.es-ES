---
title: Artista
description: Informa sobre el contenido de audio del artista intérprete o ejecutante.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 10%

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
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoaudioartist` |
| Audience Manager | `c_contextdata.a.media.artist` |

## Elementos de dimensión

Cada elemento es el nombre literal del intérprete registrado al inicio de la sesión. Utilice un nombre canónico estable por artista para que los datos no se fragmenten en las variantes de formato.
