---
title: Nombre de pod
description: Informa del nombre descriptivo de cada pausa publicitaria. Recopile datos en Adobe Analytics mediante una clasificación o una regla de procesamiento personalizada.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---


# Nombre de pod

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Nombre de la secuencia**. Consulte [Nombre de la pausa publicitaria](/help/implementation/variables/ads/ad-break-name.md) para ver cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Nombre de secuencia** indica el nombre descriptivo de cada pausa publicitaria (por ejemplo, `"pre-roll"`, `"mid-roll-1"`). En Customer Journey Analytics es una dimensión discreta rellenada directamente desde la variable de implementación. En Adobe Analytics está disponible a través de dos métodos: una clasificación de la dimensión [Ad pod](ad-pod.md) o un eVar que se rellena mediante una regla de procesamiento.

## Cómo se rellena esta dimensión

El nombre de la secuencia proviene del valor [Nombre de la pausa publicitaria](/help/implementation/variables/ads/ad-break-name.md) que el reproductor establece en [inicio de la pausa publicitaria](/help/implementation/events/ads/ad-break-start.md).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics (regla de procesamiento) | Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.ad.podFriendlyName` a un eVar. |
| Adobe Analytics (clasificación) | Clasificación de la dimensión de pod de anuncios: Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.ad.podFriendlyName`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.ad.podFriendlyName` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación del nombre de la secuencia cuando **[[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método proporciona una relación garantizada de 1:1 entre cada ID de pod y su nombre descriptivo. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de clasificación del nombre de la secuencia. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.ad.podFriendlyName` a un eVar. Este método captura el nombre descriptivo como un valor por visita sin requerir mantenimiento de clasificación.

La solución es que se pierde la relación garantizada 1:1 entre el nombre del pod y la dimensión [pod de anuncios](ad-pod.md) principal. Si la implementación envía valores incoherentes para el mismo ID de pod a través de los eventos, pueden aparecer varios nombres bajo el mismo pod de anuncios. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es el nombre literal de la pausa publicitaria registrado en [inicio de la pausa publicitaria](/help/implementation/events/ads/ad-break-start.md).
