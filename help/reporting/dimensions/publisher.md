---
title: Editor
description: Informa del editor del contenido de audio.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

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
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.publisher` cuando [[!UICONTROL Metadatos de audio]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## Elementos de dimensión

Cada elemento es el nombre literal del publicador registrado al inicio de la sesión.
