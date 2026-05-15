---
title: Show
description: Informa del nombre del programa o la serie del contenido de vídeo que forma parte de una serie.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 8%

---


# Show

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Mostrar**. Consulte [Mostrar](/help/implementation/variables/standard-metadata/show.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Mostrar** indica el nombre del programa o serie. Los episodios de varias temporadas se acumulan en el mismo elemento de línea de programa, por lo que debe utilizarlo para comparar la participación a lo largo de toda la duración de una serie.

## Cómo se rellena esta dimensión

El reproductor establece el programa al principio de la sesión cuando el contenido forma parte de una serie.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.show` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## Elementos de dimensión

Cada elemento es el nombre literal para mostrar indicado al inicio de la sesión (por ejemplo, `"Blinding Light"`). Utilice nombres diferentes y estables por programa para que los datos no se contraigan en programas no relacionados que compartan una palabra.
