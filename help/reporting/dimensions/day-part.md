---
title: Parte del día
description: Notifica la hora del día (mañana, tarde, hora de mayor audiencia, noche más tarde) en que se emitió o reprodujo el contenido.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 6%

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
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.dayPart` cuando [[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videodaypart, post_videodaypart` |

## Elementos de dimensión

Cada elemento es la etiqueta de partición de día literal registrada al inicio de la sesión. Utilice un conjunto fijo de valores en todas las implementaciones para mantener la coherencia de los elementos de línea.
