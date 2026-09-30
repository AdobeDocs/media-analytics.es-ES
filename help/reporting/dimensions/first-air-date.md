---
title: Primera fecha de emisión
description: Informa de la fecha en la que el contenido se emitió por primera vez en televisión.
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
source-wordcount: '403'
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
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Contenido (ID)](content.md). Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.airDate`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.airDate` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación First air date cuando **[[!UICONTROL Video Metadata]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método garantiza una relación 1:1 entre cada ID de contenido y su primera fecha de emisión. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de la clasificación First air date. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.airDate` a un eVar. Este método registra la primera fecha de emisión como un valor por visita sin necesidad de realizar un mantenimiento de clasificación.

La compensación es que pierde la relación 1:1 garantizada entre la primera fecha de emisión y la dimensión principal [Contenido (ID)](content.md). Si la implementación envía valores incoherentes para el mismo ID de contenido entre eventos, pueden aparecer varias fechas de publicación bajo el mismo contenido. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es la cadena de fecha literal notificada al inicio de la sesión. Utilice un formato coherente en todas las implementaciones. Adobe recomienda `YYYY-MM-DD`.
