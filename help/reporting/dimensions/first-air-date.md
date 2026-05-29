---
title: Primera fecha de emisión
description: Informa de la fecha en la que el contenido se emitió por primera vez en televisión.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---


# Primera fecha de emisión

>[!BEGINSHADEBOX]

*Esta página cubre la **Primera fecha de emisión**&#x200B;dimensión del informe. Consulte [Primera fecha de emisión](/help/implementation/variables/standard-metadata/first-air-date.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Primera fecha de emisión** indica la fecha en la que se emitió por primera vez el contenido en televisión. Utilícelo para separar la participación en nuevas versiones de la participación en contenido antiguo.

## Cómo se rellena esta dimensión

La primera fecha de emisión la establece el reproductor al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics (regla de procesamiento) | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.airDate` a un eVar. |
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Contenido (ID)](content.md): Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.airDate`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.airDate` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación First air date cuando **[[!UICONTROL Video Metadata]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método garantiza una relación de 1:1 entre cada ID de contenido y su primera fecha de emisión. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de la clasificación First air date. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.airDate` a un eVar. Este método registra la primera fecha de emisión como un valor por visita sin necesidad de realizar un mantenimiento de clasificación.

La compensación es que pierde la relación garantizada 1:1 entre la primera fecha de emisión y la dimensión principal [Contenido (ID)](content.md). Si la implementación envía valores incoherentes para el mismo ID de contenido entre eventos, pueden aparecer varias fechas de publicación bajo el mismo contenido. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es la cadena de fecha literal notificada al inicio de la sesión. Utilice un formato coherente en todas las implementaciones. Adobe recomienda `YYYY-MM-DD`.
