---
title: Nombre del capítulo
description: Muestra el título del capítulo legible en lenguaje natural.
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
source-wordcount: '367'
ht-degree: 2%
---

# Nombre del capítulo

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Nombre del capítulo**. Consulte [Nombre de capítulo](/help/implementation/variables/chapters/chapter-name.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Nombre de capítulo** muestra el título legible en lenguaje natural de cada capítulo (por ejemplo, `"Pilot Episode - Opening"`).

## Cómo se rellena esta dimensión

El reproductor establece el nombre del capítulo en cada evento de [inicio del capítulo](/help/implementation/events/chapters/chapter-start.md).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics (regla de procesamiento) | Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.chapter.friendlyName` a un eVar. |
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Chapter](chapter.md). Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Capítulos multimedia]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.chapter.friendlyName`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.chapter.friendlyName` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación de nombres de capítulos cuando **[[!UICONTROL Capítulos multimedia]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método garantiza una relación 1:1 entre cada ID de capítulo y su nombre descriptivo. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de clasificación del nombre del capítulo. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.chapter.friendlyName` a un eVar. Este método captura el nombre descriptivo como un valor por visita sin requerir mantenimiento de clasificación.

El equilibrio es que se pierde la relación 1:1 garantizada entre el nombre del capítulo y la dimensión [Chapter](chapter.md) principal. Si la implementación envía valores incoherentes para el mismo ID de capítulo a través de los eventos, pueden aparecer varios nombres en el mismo capítulo. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es el título literal del capítulo registrado en [inicio del capítulo](/help/implementation/events/chapters/chapter-start.md).
