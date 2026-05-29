---
title: Primera fecha digital
description: Informa de la fecha en la que el contenido apareció por primera vez en una plataforma digital.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# Primera fecha digital

>[!BEGINSHADEBOX]

*Esta página cubre la **Primera fecha digital**dimensión de informe. Consulte [Primera fecha digital](/help/implementation/variables/standard-metadata/first-digital-date.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Primera fecha digital** indica la fecha en la que el contenido apareció por primera vez en una plataforma digital. Utilícelo junto con [Primera fecha de emisión](first-air-date.md) para comparar el tiempo de lanzamiento digital con la emisión original.

## Cómo se rellena esta dimensión

La primera fecha digital la establece el reproductor al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics (regla de procesamiento) | Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.digitalDate` a un eVar. |
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Contenido (ID)](content.md): Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.digitalDate`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.digitalDate` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura Primera clasificación de fecha digital cuando **[[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método garantiza una relación 1:1 entre cada ID de contenido y su primera fecha digital. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el Nombre de la primera clasificación de fecha digital. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.digitalDate` a un eVar. Este método captura la primera fecha digital como un valor por visita sin requerir mantenimiento de clasificación.

El equilibrio es que pierde la relación garantizada 1:1 entre la primera fecha digital y la dimensión principal [Contenido (ID)](content.md). Si la implementación envía valores incoherentes para el mismo ID de contenido entre eventos, pueden aparecer varias primeras fechas digitales bajo el mismo contenido. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es la cadena de fecha literal notificada al inicio de la sesión. Utilice un formato coherente en todas las implementaciones. Adobe recomienda `YYYY-MM-DD`.
