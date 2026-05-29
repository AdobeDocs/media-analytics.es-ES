---
title: Segmento de contenido
description: Informa del rango del cabezal de reproducción visto durante una sesión, en minutos.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 6%

---


# Segmento de contenido

La dimensión **Segmento de contenido** indica el intervalo del cabezal de reproducción que se vio durante una sesión en minutos (por ejemplo, `[0-5]` para los minutos del 0 al 5). El servidor calcula el segmento a partir de los valores mínimo y máximo del cabezal de reproducción registrados durante la reproducción. Utilícelo junto con la métrica [Vistas de segmentos de contenido](/help/reporting/metrics/content-segment-views.md) para analizar qué partes de visualizadores de contenido de formato largo consumen realmente.

## Cómo se rellena esta dimensión

El back-end de medios calcula el segmento de contenido a partir de los valores del cabezal de reproducción informados en los eventos de la sesión. El cliente no lo establece. El valor del informe se deriva de los valores del cabezal de reproducción vistos durante la reproducción.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics | Se recopila automáticamente a partir de los datos de contexto `a.media.segment` cuando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.segment`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos | `videosegment`, `post_videosegment` |
| Audience Manager | `c_contextdata.a.media.segment` |

>[!IMPORTANT]
>
>Si el cabezal de reproducción no se registra correctamente durante la sesión, el segmento calculado puede ser inexacto. Para los flujos en directo, el segmento se calcula a partir de los valores relativos del cabezal de reproducción vistos durante la sesión.

## Elementos de dimensión

Cada elemento es un intervalo de cadenas que cubre los valores del cabezal de reproducción vistos durante una sesión (por ejemplo, `[0-5]`, `[5-10]`, `[10-15]`). La granularidad se fija en cinco minutos.
