---
title: Configuración de Chromecast para medios de streaming
description: Instale y configure Media SDK para Chromecast para implementaciones de medios de streaming solo de Analytics.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
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
