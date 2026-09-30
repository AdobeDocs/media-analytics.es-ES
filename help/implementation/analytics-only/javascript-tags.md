---
title: Configuración de la extensión de etiquetas de Media Analytics
description: Utilice la extensión de Adobe Media Analytics (3.x SDK) para audio y vídeo para implementar medios de streaming solo de Analytics.
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
source-wordcount: '242'
ht-degree: 12%
---
# Configuración de la extensión de etiquetas de Media Analytics

La extensión de etiquetas de Adobe Media Analytics (3.x SDK) para audio y vídeo implementa Media SDK para JavaScript (3.x) mediante etiquetas, sin necesidad de realizar una instalación manual de JavaScript. Esta página cubre la configuración de Etiquetas. Para instalar SDK en código, consulta [Configurar JavaScript para medios de streaming](javascript.md). Para nuevas implementaciones, considere la ruta de Edge [extensión de etiquetas Web SDK](/help/implementation/edge/web-sdk-tags.md) recomendada.

* **Requisitos previos**: complete la [descripción general de la implementación solo de Analytics](overview.md).

## Instalación y configuración de la extensión de

Añada la instancia de Media Tracker a un sitio con etiquetas habilitadas instalando y configurando la extensión en la interfaz de usuario de la recopilación de datos. Para obtener detalles de instalación y configuración, consulte [Extensión de Adobe Media Analytics (3.x SDK) para audio y vídeo](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=es).

## Seguimiento de eventos de medios

Con la extensión configurada, rastree cada evento de medios con su método de rastreador. Consulte la pestaña **Media SDK JS 3.x** en cada página de [evento](/help/implementation/events/overview.md) y [variable](/help/implementation/variables/overview.md) para ver las llamadas exactas.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones solo de Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Extensión de Adobe Media Analytics (3.x SDK) para audio y vídeo](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=es)
>* [Configurar JavaScript para medios de transmisión (en código)](javascript.md)
>* [Resumen de eventos](/help/implementation/events/overview.md)
