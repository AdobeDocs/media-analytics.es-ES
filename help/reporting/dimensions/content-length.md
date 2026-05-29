---
title: Longitud de contenido
description: Notifica la duración total en segundos de cada sesión de contenido, según se establece al inicio de la sesión.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 6%

---


# Longitud de contenido

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Longitud del contenido**. Consulte [Longitud del contenido](/help/implementation/variables/core/content-length.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Longitud del contenido** indica la duración total en segundos de cada sesión de contenido según se establece al inicio de la sesión. Activa las métricas back-end, incluidos [marcadores de progreso](/help/reporting/metrics/progress-markers.md) y [Audiencia media por minuto](/help/reporting/metrics/average-minute-audience.md).

## Cómo se rellena esta dimensión

El reproductor establece la longitud del contenido al inicio de la sesión. El valor del informe es la duración completa del recurso en segundos, no el cabezal de reproducción transcurrido.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.length` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videolength`, `post_videolength` |
| Audience Manager | `c_contextdata.a.media.length` |

>[!NOTE]
>
>En Adobe Analytics, este valor también corresponde a una clasificación **Video length** en la dimensión [Contenido](content.md). Usted es responsable de rellenar y mantener esa clasificación por separado. Customer Journey Analytics utiliza esta dimensión directamente. Si lo desea, puede utilizar [Clasificación de valores](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/value-bucketing).

>[!IMPORTANT]
>
>Si la longitud del contenido no está establecida o no es mayor que cero, los marcadores de progreso y la audiencia media por minuto no se generan para esa sesión. Para emisiones en directo de duración desconocida, establezca `86400`.

## Elementos de dimensión

Cada elemento es el valor de longitud literal, en segundos, registrado al inicio de la sesión.
