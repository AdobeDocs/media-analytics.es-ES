---
title: Desplazamiento de capítulo
description: Informa del desplazamiento de cada capítulo dentro del contenido.
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
source-wordcount: '376'
ht-degree: 2%
---

# Desplazamiento de capítulo

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Desplazamiento de capítulo**. Consulte [Desplazamiento de capítulo](/help/implementation/variables/chapters/chapter-offset.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Desplazamiento de capítulo** indica el desplazamiento de cada capítulo dentro del contenido, medido en segundos desde el inicio.

## Cómo se rellena esta dimensión

El reproductor establece el desplazamiento del capítulo en cada evento de [inicio del capítulo](/help/implementation/events/chapters/chapter-start.md).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics (regla de procesamiento) | Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.chapter.offset` a un eVar. |
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Chapter](chapter.md). Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Capítulos multimedia]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.chapter.offset`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.chapter.offset` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación de desplazamiento de capítulo cuando **[[!UICONTROL Capítulos multimedia]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método garantiza una relación 1:1 entre cada ID de capítulo y su desplazamiento. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de clasificación de desvío de capítulo. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.chapter.offset` a un eVar. Este método captura el desplazamiento del capítulo como un valor por visita sin requerir mantenimiento de clasificación.

La compensación es que se pierde la relación 1:1 garantizada entre el desplazamiento del capítulo y la dimensión [Chapter](chapter.md) principal. Si la implementación envía valores incoherentes para el mismo ID de capítulo a través de los eventos, pueden aparecer varios desplazamientos en el mismo capítulo. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es el valor de desplazamiento entero, en segundos, registrado el [inicio del capítulo](/help/implementation/events/chapters/chapter-start.md).
