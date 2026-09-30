---
title: Parte del día
description: Notifica la hora del día (mañana, tarde, hora de mayor audiencia, noche más tarde) en que se emitió o reprodujo el contenido.
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
source-wordcount: '151'
ht-degree: 9%
---

# Parte del día

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Parte del día**. Consulte [Parte del día](/help/implementation/variables/standard-metadata/day-part.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Parte del día** indica el período de tiempo del día en el que se emitió o reprodujo el contenido. Los valores comunes son `"Morning"`, `"Afternoon"`, `"Primetime"` y `"Late Night"`. Utilícelo para comparar la participación en varias partes del día independientemente de la zona horaria local del visualizador.

## Cómo se rellena esta dimensión

El reproductor establece la parte del día al comienzo de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.dayPart` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videodaypart`, `post_videodaypart` |
| Audience Manager | `c_contextdata.a.media.dayPart` |

## Elementos de dimensión

Cada elemento es la etiqueta de partición de día literal registrada al inicio de la sesión. Utilice un conjunto fijo de valores en todas las implementaciones para mantener la coherencia de los elementos de línea.
