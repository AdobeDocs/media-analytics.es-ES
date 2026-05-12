---
title: Posición del capítulo
description: Informa del índice de cada capítulo dentro del contenido.
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 1%

---


# Posición del capítulo

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Posición del capítulo**. Consulte [Posición del capítulo](/help/implementation/variables/chapters/chapter-position.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Posición del capítulo** indica el índice de cada capítulo dentro del contenido.

## Cómo se rellena esta dimensión

El reproductor establece la posición del capítulo en cada evento de `media.chapterStart`.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics (regla de procesamiento) | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.chapter.position` a un eVar. |
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Chapter](chapter.md): Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.index`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.chapter.position`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación de la posición del capítulo cuando **[[!UICONTROL Capítulos multimedia]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método proporciona una relación garantizada de 1:1 entre cada ID de capítulo y su posición. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de clasificación de la posición del capítulo. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.chapter.position` a un eVar. Este método registra la posición del capítulo como un valor por visita sin requerir mantenimiento de clasificación.

El equilibrio es que se pierde la relación garantizada 1:1 entre la posición del capítulo y la dimensión principal [Chapter](chapter.md). Si la implementación envía valores incoherentes para el mismo ID de capítulo a través de los eventos, pueden aparecer varias posiciones bajo el mismo capítulo. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es el valor de posición entero registrado en `media.chapterStart`.
