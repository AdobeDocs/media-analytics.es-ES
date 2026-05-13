---
title: Episodio
description: Informa del número del episodio dentro de una temporada.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 9%

---


# Episodio

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Episodio**. Consulte [Episodio](/help/implementation/variables/standard-metadata/episode.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Episodio** indica el número de episodio dentro de una temporada. Utilícelo junto con [Show](show.md) y [Season](season.md) para lograr participación a nivel de episodio individual.

## Cómo se rellena esta dimensión

El reproductor establece el episodio al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.episode` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoepisode, post_videoepisode` |

## Elementos de dimensión

Cada elemento es el valor literal del episodio notificado al inicio de la sesión (normalmente un entero de cadena como `"13"`). Los números de episodio por sí solos no son únicos en todas las temporadas; combine con Season para obtener desgloses inequívocos.
