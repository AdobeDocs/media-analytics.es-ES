---
title: Posición del pod
description: Informa del desplazamiento de cada desglose de anuncios dentro del contenido.
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

# Posición del pod

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Posición de la secuencia**. Consulte [Hora de inicio de la pausa publicitaria](/help/implementation/variables/ads/ad-break-start-time.md) para saber cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Posición de la secuencia** indica el desplazamiento de cada salto de anuncio dentro del contenido, en segundos. Un pre-roll tiene la posición `0`; los mid-rolls tienen posiciones correspondientes a su hora de inicio del cabezal de reproducción.

## Cómo se rellena esta dimensión

La posición de la secuencia se establece a partir del valor de [hora de inicio de la pausa publicitaria](/help/implementation/variables/ads/ad-break-start-time.md) que el reproductor establece en [inicio de la pausa publicitaria](/help/implementation/events/ads/ad-break-start.md).

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics (regla de procesamiento) | Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.ad.podSecond` a un eVar. |
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Ad pod](ad-pod.md). Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.ad.podSecond`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.ad.podSecond` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación de la posición del pod cuando **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método proporciona una relación 1:1 garantizada entre cada ID de pod de anuncios y su posición. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de clasificación de la posición de la secuencia. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.ad.podSecond` a un eVar. Este método captura la posición del pod como un valor por visita sin requerir mantenimiento de clasificación.

El equilibrio es que se pierde la relación 1:1 garantizada entre la posición del pod y la dimensión [pod de anuncios](ad-pod.md) principal. Si la implementación envía valores incoherentes para el mismo ID de pod a través de los eventos, pueden aparecer varias posiciones bajo el mismo pod de anuncios. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es el valor de desplazamiento entero (en segundos) registrado en [inicio de pausa publicitaria](/help/implementation/events/ads/ad-break-start.md).
