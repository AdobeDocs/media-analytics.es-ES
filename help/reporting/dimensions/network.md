---
title: Red
description: Informa del nombre del canal o la red de difusión.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 9%

---


# Red

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Red**. Consulte [Red](/help/implementation/variables/standard-metadata/network.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Red** indica el nombre de la red o canal de difusión (por ejemplo, `"Fox"` o `"ESPN"`). Utilícelo para comparar la participación en redes dentro de la misma propiedad de flujo continuo.

## Cómo se rellena esta dimensión

El reproductor establece la red al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.network` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videonetwork, post_videonetwork` |

## Elementos de dimensión

Cada elemento es el valor de red literal notificado al inicio de la sesión. Utilice un nombre estable y distinto por red para que los datos no se fragmenten en las distintas variantes ortográficas.
