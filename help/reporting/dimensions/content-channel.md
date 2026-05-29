---
title: Canal de contenido
description: Informa de la estación de distribución, red o propiedad donde se reprodujo cada sesión.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 7%

---


# Canal de contenido

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Canal de contenido**. Consulte [Canal de contenido](/help/implementation/variables/core/content-channel.md) para saber cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Canal de contenido** indica la estación de distribución, red o propiedad donde se reprodujo cada sesión. Utilícela para dividir la reproducción por red o sección de una propiedad.

## Cómo se rellena esta dimensión

El reproductor establece el canal al inicio de la sesión y persiste durante la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.channel` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>Si no se establece el canal, la dimensión no se rellena para esa sesión.

## Elementos de dimensión

Cada elemento es la cadena literal establecida al inicio de la sesión. Se acepta cualquier cadena. Los valores habituales son un nombre de red, una parte de una ruta de sitio o un identificador de propiedad interno.
