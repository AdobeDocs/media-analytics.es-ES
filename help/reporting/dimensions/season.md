---
title: Temporada
description: Informa del número de temporada del contenido episódico.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 10%

---


# Temporada

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Temporada**. Consulte [Temporada](/help/implementation/variables/standard-metadata/season.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Temporada** indica el número de temporada del contenido episódico. Úsalo junto con [Show](show.md) y [Episode](episode.md) para episodios completos.

## Cómo se rellena esta dimensión

La temporada la establece el reproductor al inicio de la sesión cuando el contenido forma parte de una serie.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.season` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoseason`, `post_videoseason` |
| Audience Manager | `c_contextdata.a.media.season` |

## Elementos de dimensión

Cada elemento es el valor de temporada literal notificado al inicio de la sesión (normalmente un entero de cadena como `"1"`, `"2"`). Sea coherente en todos los episodios dentro del mismo programa; la dimensión no normaliza `"1"` y `"01"` al mismo elemento de línea.
