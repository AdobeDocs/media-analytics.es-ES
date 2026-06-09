---
title: Resumen de implementación solo de Analytics
description: Requisitos previos y métodos de implementación del complemento de Adobe Analytics para medios de streaming, utilizado en implementaciones solo de Analytics.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '234'
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
| API | [API de recopilación de medios](media-collection-api.md) | — |

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones solo de Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Descripción general de la implementación](/help/implementation/overview.md)
>* [Resumen de eventos](/help/implementation/events/overview.md)
>* [Resumen de variables](/help/implementation/variables/overview.md)
