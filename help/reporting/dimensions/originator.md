---
title: Creador
description: Informa al creador o estudio de producción del contenido.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '385'
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
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Contenido (ID)](content.md): Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.originator`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.originator`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.originator` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación del creador cuando **[[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método garantiza una relación de 1:1 entre cada ID de contenido y su creador. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de la clasificación de creador. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.originator` a un eVar. Este método registra el creador como un valor por visita sin requerir mantenimiento de clasificación.

La solución es que pierde la relación garantizada 1:1 entre el creador y la dimensión principal [Contenido (ID)](content.md). Si la implementación envía valores incoherentes para el mismo ID de contenido entre eventos, pueden aparecer varios creadores bajo el mismo contenido. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es el valor de originador literal registrado al inicio de la sesión. Utilice un nombre estable y distinto por estudio para que la participación no se contraiga en entidades no relacionadas.
