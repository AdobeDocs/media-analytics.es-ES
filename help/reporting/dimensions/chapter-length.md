---
title: Longitud del capítulo
description: Informa de la duración de cada capítulo.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---


# Longitud del capítulo

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Longitud del capítulo**. Consulte [Longitud del capítulo](/help/implementation/variables/chapters/chapter-length.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Longitud del capítulo** indica la duración de cada capítulo en segundos.

## Cómo se rellena esta dimensión

El reproductor establece la longitud del capítulo en cada evento de [inicio del capítulo](/help/implementation/events/chapters/chapter-start.md).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics (regla de procesamiento) | Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.chapter.length` a un eVar. |
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Chapter](chapter.md): Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Media Chapters]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.chapter.length`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.chapter.length` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación de la longitud del capítulo cuando **[[!UICONTROL Capítulos multimedia]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método proporciona una relación garantizada de 1:1 entre cada ID de capítulo y su longitud. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de la clasificación de longitud del capítulo. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.chapter.length` a un eVar. Este método captura la longitud del capítulo como un valor por visita sin requerir mantenimiento de clasificación.

El equilibrio es que se pierde la relación garantizada 1:1 entre la longitud del capítulo y la dimensión principal [Chapter](chapter.md). Si la implementación envía valores incoherentes para el mismo ID de capítulo a través de eventos, pueden aparecer varias longitudes bajo el mismo capítulo. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es el valor de longitud total, en segundos, registrado el [inicio del capítulo](/help/implementation/events/chapters/chapter-start.md).
