---
title: Configurar la API de recopilación de medios para los medios de streaming
description: Utilice la API de recopilación de medios para enviar datos de medios de streaming directamente a Adobe Analytics con llamadas HTTP RESTful.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

---

# Configurar la API de recopilación de medios para los medios de streaming

La API de recopilación de medios envía datos de medios de streaming directamente a Adobe Analytics mediante llamadas HTTP RESTful. Como es totalmente personalizable, admite seguimiento personalizado y dispositivos que los SDK no cubren. Utilícelo cuando una SDK no sea una opción para su plataforma.

* **Requisitos previos**: complete la [descripción general de la implementación solo de Analytics](overview.md).

## Implementación de la API

Abra una sesión con una solicitud `sessionStart` y envíe los eventos subsiguientes a la sesión que devuelva. Para obtener los formatos de solicitud/respuesta completos, los parámetros, los esquemas de validación y las instrucciones de implementación, consulte la [Referencia de la API de Media Collection](../media-collection-api/mc-api-overview.md).

## Seguimiento de eventos de medios

Consulte la pestaña **API de recopilación de medios** en cada [evento](/help/implementation/events/overview.md) y página de [variable](/help/implementation/variables/overview.md) para ver las cargas exactas.

## Siguiente paso

Una vez completada la implementación, puede [configurar informes para implementaciones solo de Analytics](/help/reporting/setup/analytics-reporting.md).

>[!MORELIKETHIS]
>
>* [Referencia de la API de Media Collection](../media-collection-api/mc-api-overview.md)
>* [Resumen de eventos](/help/implementation/events/overview.md)
>* [Resumen de variables](/help/implementation/variables/overview.md)
