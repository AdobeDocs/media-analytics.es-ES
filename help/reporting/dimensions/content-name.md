---
title: Nombre de contenido
description: Informa del título en lenguaje natural de cada sesión multimedia.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 8%

---


# Nombre de contenido

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Nombre del contenido**. Consulte [Nombre de contenido](/help/implementation/variables/core/content-name.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Nombre de contenido** indica el título legible en lenguaje natural de cada sesión multimedia.

## Cómo se rellena esta dimensión

El nombre descriptivo lo establece el reproductor al inicio de la sesión. El valor del informe coincide con el que se envió.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.friendlyName` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoname, post_videoname` |

>[!NOTE]
>
>En Adobe Analytics, este valor también corresponde a una clasificación **Video name** en la dimensión [Contenido](content.md). Usted es responsable de rellenar y mantener esa clasificación por separado. Customer Journey Analytics utiliza esta dimensión directamente.

>[!IMPORTANT]
>
>Si no se establece el nombre del contenido, la dimensión no se rellena para esa sesión.

## Elementos de dimensión

Cada elemento es el título literal registrado al inicio de la sesión (por ejemplo, `"Blinding Light"`).
