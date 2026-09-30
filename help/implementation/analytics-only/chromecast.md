---
title: Configuración de Chromecast para medios de streaming
description: Instale y configure Media SDK para Chromecast para implementaciones de medios de streaming solo de Analytics.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 10%
---
# Configuración de Chromecast para medios de streaming

Media SDK para Chromecast envía datos de medios de streaming desde las aplicaciones receptoras de Chromecast directamente a Adobe Analytics. SDK y su documentación están alojados en GitHub.

* **Requisitos previos**:
  * Complete la [descripción general de la implementación solo de Analytics](overview.md).
  * [Descargar Media SDK para Chromecast](/help/getting-started/download-sdks.md).

## Instalación y configuración de SDK

Añada SDK a la aplicación del receptor de Chromecast y configure el rastreador como se describe en las referencias canónicas:

* [Configuración de Chromecast SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md)
* [Referencia de la API de Chromecast SDK](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)

## Seguimiento de eventos de medios

Con el rastreador creado, rastree cada evento de medios mediante su método de rastreador. Consulte la pestaña **Chromecast** en cada página de [event](/help/implementation/events/overview.md) y [variable](/help/implementation/variables/overview.md) para ver las llamadas exactas.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones solo de Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Referencia de la API de Chromecast SDK](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/)
>* [Resumen de eventos](/help/implementation/events/overview.md)
>* [Resumen de variables](/help/implementation/variables/overview.md)
