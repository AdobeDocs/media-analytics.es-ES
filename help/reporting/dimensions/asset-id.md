---
title: ID del recurso
description: Informa de un identificador estable del sector para el recurso de medios subyacente.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---


# ID del recurso

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **ID de recurso**. Consulte [ID de recurso](/help/implementation/variables/standard-metadata/asset-id.md) para saber cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **ID del recurso** indica un identificador estable del sector para el recurso de medios subyacente (normalmente un ID de EIDR, TMS/Gracenote o ID de Rovi, pero también se aceptan los ID propietarios).

## Cómo se rellena esta dimensión

El reproductor establece el ID de recurso al inicio de la sesión.

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics (regla de procesamiento) | Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.asset` a un eVar. |
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Contenido (ID)](content.md): Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.asset`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.asset` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación de ID de recurso cuando **[[!UICONTROL Metadatos de vídeo]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método garantiza una relación de 1:1 entre cada ID de contenido y su ID de recurso. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de la clasificación del ID de recurso. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.asset` a un eVar. Este método captura el ID de recurso como un valor por visita sin requerir mantenimiento de clasificación.

La solución es que pierde la relación garantizada 1:1 entre el ID del recurso y la dimensión principal [Contenido (ID)](content.md). Si la implementación envía valores incoherentes para el mismo ID de contenido entre eventos, pueden aparecer varios ID de recurso bajo el mismo contenido. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es un valor de ID de recurso único registrado durante el periodo del informe. Utilice un único identificador estable por recurso en todas las plataformas de distribución para que el mismo contenido se reúna en un solo elemento de línea.
