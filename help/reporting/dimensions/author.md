---
title: Autor
description: Informa sobre el autor del contenido. Se utiliza principalmente para audiolibros.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 10%

---


# Autor

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Autor**. Consulte [Autor](/help/implementation/variables/standard-metadata/author.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Autor** informa sobre el autor del contenido (por ejemplo, `"Eleanor Clementine"`). Se utiliza principalmente para audiolibros, pero también es válido para podcasts cuyo host o productor es la atribución relevante.

## Cómo se rellena esta dimensión

El reproductor establece el autor al inicio de la sesión para el contenido de audio.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.author` cuando [[!UICONTROL Metadatos de audio]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoaudioauthor` |

## Elementos de dimensión

Cada elemento es el nombre literal del autor registrado al inicio de la sesión.
