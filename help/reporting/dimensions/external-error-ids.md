---
title: ID de error externo
description: Notifica identificadores de error únicos de fuentes externas como errores de CDN.
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
source-wordcount: '155'
ht-degree: 7%
---

# ID de error externo

La dimensión **ID de error externo** informa de identificadores de error únicos de cualquier fuente fuera de SDK del reproductor (por ejemplo, errores de CDN). El reproductor debe proporcionar los códigos o ID en el momento de la implementación mediante la API de seguimiento de errores. Se admiten varios ID de error por sesión.

## Cómo se rellena esta dimensión

El reproductor pasa los ID de error externos al rastreador en [eventos de error](/help/implementation/events/error.md). El servidor recopila ID únicos en toda la sesión y los comunica en la llamada de cierre.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.qoe.externalErrors` cuando [[!UICONTROL Calidad de los medios]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.externalErrors`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Fuentes de datos | `videoqoeextneralerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.externalErrors` |

## Elementos de dimensión

Cada elemento es un código de error o ID proporcionado por el reproductor. Utilice una taxonomía estable en todas las implementaciones para que los ID de error se resuman correctamente en las sesiones.
