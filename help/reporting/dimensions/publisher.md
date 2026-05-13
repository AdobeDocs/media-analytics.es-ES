---
title: Editor
description: Informa del editor del contenido de audio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 10%

---


# Editor

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informes de **Publicador**. Consulte [Publicador](/help/implementation/variables/standard-metadata/publisher.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Publicador** informa del publicador de contenido de audio (por ejemplo, un publicador de audiolibros o una red de podcast). Utilícelo para comparar la participación de varios editores en un catálogo de audio depurado.

## Cómo se rellena esta dimensión

Publisher lo establece el reproductor al inicio de la sesión para el contenido de audio.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.publisher` cuando [[!UICONTROL Metadatos de audio]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoaudiopublisher` |

## Elementos de dimensión

Cada elemento es el nombre literal del publicador registrado al inicio de la sesión.
