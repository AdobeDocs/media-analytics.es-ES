---
title: Calificación de contenido
description: Informa de la clasificación de audiencias según lo definido por las pautas de clasificación parental de TV o un sistema de clasificación regional.
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
source-wordcount: '400'
ht-degree: 2%
---

# Calificación de contenido

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Clasificación del contenido**. Consulte [Clasificación del contenido](/help/implementation/variables/standard-metadata/content-rating.md) para ver cómo se recopila esta variable.*

>[!ENDSHADEBOX]

La dimensión **Clasificación del contenido** indica la clasificación de audiencia de cada sesión. Utilícela para comparar la participación y la carga de anuncios en los distintos niveles de clasificación.

## Cómo se rellena esta dimensión

La clasificación de contenido la establece el reproductor al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics (regla de procesamiento) | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.rating` a un eVar. |
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Contenido (ID)](content.md). Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.rating`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.rating`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.rating` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación Clasificación de clasificación de clasificación de contenido cuando **[[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método garantiza una relación 1:1 entre cada ID de contenido y su clasificación. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de la clasificación de clasificación de clasificación de clasificación de contenido. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.rating` a un eVar. Este método registra la clasificación del contenido como un valor por visita sin requerir mantenimiento de clasificación.

La solución es que se pierde la relación 1:1 garantizada entre la clasificación de contenido y la dimensión [Contenido (ID)](content.md) principal. Si la implementación envía valores incoherentes para el mismo ID de contenido entre eventos, pueden aparecer varias clasificaciones bajo el mismo contenido. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es el valor de clasificación literal notificado al inicio de la sesión (por ejemplo, `"TVY"`, `"TVG"`, `"TVPG"`, `"TVMA"`). Conserve un conjunto fijo de valores por sistema de clasificación para evitar la fragmentación de los elementos de línea.
