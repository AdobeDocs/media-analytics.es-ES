---
title: Autor
description: Informa sobre el autor del contenido. Se utiliza principalmente para audiolibros.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 11%

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
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.author` cuando [[!UICONTROL Metadatos de audio]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoaudioauthor` |
| Audience Manager | `c_contextdata.a.media.author` |

## Elementos de dimensión

Cada elemento es el nombre literal del autor registrado al inicio de la sesión.
