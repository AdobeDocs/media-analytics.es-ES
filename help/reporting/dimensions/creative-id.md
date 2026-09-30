---
title: ID del creativo
description: Informa del identificador creativo de publicidad.
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
source-wordcount: '378'
ht-degree: 3%
---

# ID del creativo

>[!BEGINSHADEBOX]

*Esta página cubre la dimensión de informe **Creative ID**. Consulte [Creative ID](/help/implementation/variables/ads/creative-id.md) para saber cómo recopilar esta variable.*

>[!ENDSHADEBOX]

La dimensión **Creative ID** informa del identificador creativo de publicidad. Utilice la dimensión para resumir la participación en anuncios que comparten un elemento creativo.

## Cómo se rellena esta dimensión

| Sistema de informes | Fuente |
| --- | --- |
| Adobe Analytics (regla de procesamiento) | Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.ad.creative` a un eVar. |
| Adobe Analytics (clasificación) | Clasificación de la dimensión [Ad](ad.md). Adobe crea automáticamente esta clasificación cuando **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener los valores de clasificación. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.creativeID`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Fuentes de datos (regla de procesamiento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (el eVar al que se asigna la regla de procesamiento `a.media.ad.creative`) |
| Fuentes de datos (clasificación) | N/D: las fuentes de datos no admiten clasificaciones. |
| Audience Manager | `c_contextdata.a.media.ad.creative` |

## Enfoque de clasificación

Adobe crea automáticamente la estructura de clasificación de Creative ID cuando **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)** está habilitado para el grupo de informes. Usted es responsable de rellenar y mantener la clasificación mediante [conjuntos de clasificaciones](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Este método proporciona una relación 1:1 garantizada entre cada ID de anuncio y su ID creativo. Las actualizaciones de clasificación se aplican de forma retroactiva en todos los datos históricos para ese ID.

>[!IMPORTANT]
>
>No cambie el nombre de clasificación de Creative ID. Cambiarle el nombre puede hacer que Adobe vuelva a crear la clasificación original, lo que da como resultado un duplicado.

## Método de regla de procesamiento

Cree una [regla de procesamiento](https://experienceleague.adobe.com/es/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que asigne `a.media.ad.creative` a un eVar. Este método captura el ID creativo como un valor por visita sin que sea necesario realizar un mantenimiento de clasificación.

El equilibrio es que se pierde la relación 1:1 garantizada entre el ID creativo y la dimensión [Ad](ad.md) principal. Si la implementación envía valores incoherentes para el mismo ID de anuncio a través de los eventos, pueden aparecer varios ID creativos en el mismo anuncio. La actualización de un valor solo se aplica a los datos a partir de ahora.

## Elementos de dimensión

Cada elemento es un ID creativo único. Utilice un identificador estable por creativo para que el mismo creativo se reúna en un solo elemento de línea en todas las campañas.
