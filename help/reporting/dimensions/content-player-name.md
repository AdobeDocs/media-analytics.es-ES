---
title: Nombre del reproductor de contenido
description: Informa sobre qué reproductor ha procesado cada sesión de contenido.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 7%
---

# Nombre del reproductor de contenido

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Nombre del reproductor de contenido**. Consulte [Nombre del reproductor de contenido](/help/implementation/variables/core/content-player-name.md) para saber cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Nombre del reproductor de contenido** indica qué reproductor procesó cada sesión de contenido (por ejemplo, `HTML5 Player`, `Brightcove` o `Roku Player`). Utilícelo para comparar la participación, la finalización y la calidad entre los jugadores de la misma propiedad.

## Cómo se rellena esta dimensión

El nombre del reproductor lo establece el reproductor al inicio de la sesión y persiste durante toda la sesión. El valor se envía en cada evento y se comunica en Adobe Analytics y Customer Journey Analytics.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.playerName` cuando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.playerName`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videoplayername`, `post_videoplayername` |
| Audience Manager | `c_contextdata.a.media.playerName` |

>[!IMPORTANT]
>
>Si no se ha definido el nombre del reproductor, la dimensión no se rellena para esa sesión. Las sesiones sin nombre de reproductor no se pueden desglosar por reproductor en los informes.

## Elementos de dimensión

Cada elemento es la cadena literal establecida al inicio de la sesión. Utilice un nombre estable y distinto por reproductor para que los datos de los diferentes reproductores no se contraigan en un solo elemento de línea.
