---
title: Creador
description: Informa al creador o estudio de producción del contenido.
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
source-wordcount: '387'
ht-degree: 2%
---

# Creador

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Creador**. Consulte [Originator](/help/implementation/variables/standard-metadata/originator.md) para obtener información sobre cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Creador** informa sobre el creador o estudio de producción del contenido (por ejemplo, `"Warner Brothers"` o `"Sony"`). Utilícelo para comparar la participación de distintos propietarios de contenido o titulares de derechos.

## Cómo se rellena esta dimensión

El reproductor establece el creador al principio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics (regla de procesamiento) | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.originator` a un eVar. |
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Contenido (ID)](content.md). Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.originator`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.originator`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.originator` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación del creador cuando **[[!UICONTROL Metadatos de vídeo]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método garantiza una relación individual entre cada ID de contenido y su creador. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de la clasificación de creador. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.originator` a un eVar. Este método registra el creador como un valor por visita sin requerir mantenimiento de clasificación.

El equilibrio es que se pierde la relación 1:1 garantizada entre el creador y la dimensión principal [Contenido (ID)](content.md). Si la implementación envía valores incoherentes para el mismo ID de contenido entre eventos, pueden aparecer varios creadores bajo el mismo contenido. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es el valor de originador literal registrado al inicio de la sesión. Utilice un nombre estable y distinto por estudio para que la participación no se contraiga en entidades no relacionadas.
