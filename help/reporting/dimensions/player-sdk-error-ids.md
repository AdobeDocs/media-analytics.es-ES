---
title: ID de error del reproductor SDK
description: Informa de identificadores de error únicos generados por el SDK del reproductor de contenido.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 6%

---


# ID de error del reproductor SDK

La dimensión **ID de error del reproductor SDK** indica identificadores de error únicos generados por el SDK del reproductor de contenido durante una sesión. El reproductor debe proporcionar los códigos o ID en el momento de la implementación mediante la API de seguimiento de errores. Se admiten varios ID de error por sesión.

## Cómo se rellena esta dimensión

El reproductor pasa los ID de error del reproductor-SDK al rastreador en `media.error` eventos. El servidor recopila ID únicos en toda la sesión y los comunica en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.playerSdkErrors` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoeplayersdkerrors, post_videoqoeplayersdkerrors` |

## Elementos de dimensión

Cada elemento es un código de error o ID generado por el reproductor SDK. Utilice una taxonomía estable en todas las implementaciones para que los ID de error se resuman correctamente en las sesiones.
