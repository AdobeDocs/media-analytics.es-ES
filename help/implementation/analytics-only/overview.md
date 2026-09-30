---
title: Resumen de implementación solo de Analytics
description: Requisitos previos y métodos de implementación del complemento de Adobe Analytics para medios de streaming, utilizado en implementaciones solo de Analytics.
feature: Streaming Media
role: User, Admin, Developer
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
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 5%
---
# Resumen de implementación solo de Analytics

Las implementaciones solo de Analytics utilizan el complemento Adobe Analytics para medios de streaming para enviar datos directamente a Adobe Analytics, sin Edge Network. Estos métodos siguen siendo totalmente compatibles. Para nuevas implementaciones, Adobe recomienda la [implementación de Edge](/help/implementation/edge/overview.md) en su lugar, ya que pone los datos a disposición de Customer Journey Analytics, Adobe Journey Optimizer y Real-Time CDP, además de Adobe Analytics.

## Requisitos previos

1. **Complete los requisitos previos generales.** Consulte los [requisitos previos generales](/help/getting-started/prereqs.md).

1. **Confirmar una implementación de Adobe Analytics.** Una implementación de medios de streaming solo de Analytics requiere una implementación básica de Adobe Analytics. Ver [Implementar Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=es).

1. **Obtener la URL del servidor de seguimiento de medios.** Solicite a su representante de Adobe Analytics la URL del servidor de seguimiento de medios (la URL `collection-api-server`). El dominio suele seguir el patrón `[your_namespace].hb-api.omtrdc.net`.

1. **Descargue SDK o instale la extensión.** Según la plataforma, [descargue el SDK actual](/help/getting-started/download-sdks.md) o instale la extensión de etiquetas requerida.

## Elija el método de implementación

Cada página cubre la configuración específica de los medios de streaming. El código por evento y por variable se encuentra en [Events](/help/implementation/events/overview.md) y [Variables](/help/implementation/variables/overview.md).

| Código base | En código | Uso de etiquetas |
|---|---|---|
| Web (JavaScript) | [JavaScript](javascript.md) | [Extensión de etiqueta de Media Analytics](javascript-tags.md) |
| Chromecast | [Chromecast](chromecast.md) | — |
| Roku | [Roku 2.x](roku-2x.md) | — |
| API | [API de recopilación de medios](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/implementation) | — |

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones solo de Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Descripción general de la implementación](/help/implementation/overview.md)
>* [Resumen de eventos](/help/implementation/events/overview.md)
>* [Resumen de variables](/help/implementation/variables/overview.md)
