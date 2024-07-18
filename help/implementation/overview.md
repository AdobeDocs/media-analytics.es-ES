---
title: Implementación del complemento de recopilación de medios de streaming
description: Obtenga información acerca de las rutas de implementación del complemento de recopilación de medios de streaming.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 69%

---

# Implementación del complemento de recopilación de medios de streaming

Existen varias formas de implementar el complemento Recopilación de medios de streaming de Adobe. Para ver una comparación detallada de los dispositivos y las plataformas compatibles con los métodos de implementación descritos en esta página, consulte [Dispositivos y plataformas compatibles](/help/getting-started/supported-devices.md).

## Métodos de implementación de Edge

Se recomienda utilizar Edge al implementar el complemento de recopilación de medios de streaming para todos los clientes nuevos de Adobe Analytics o de Customer Journey Analytics.

* **Media for Edge Network SDK/Extension:** recopila datos de la web, los dispositivos iOS y Android o los dispositivos Roku y los envía al Edge Network. A continuación, los datos se pueden enviar a Customer Journey Analytics o a Adobe Analytics.

  Para obtener más información acerca de la extensión/SDK de Media for Edge Network, consulte [Implementar el complemento de recopilación de medios de streaming con Edge Network](/help/implementation/edge/implementation-edge.md).

* **API de Media Edge:** se puede personalizar para recopilar datos de cualquier dispositivo o formato (incluidos dispositivos móviles, web y de servicios OTT) y enviar datos al Edge Network. A continuación, los datos se pueden enviar a Customer Journey Analytics o a Adobe Analytics.

  Para obtener más información sobre la API de Media Edge, consulte [Información general sobre la API de Media Edge](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/).

![Flujo de trabajo de CJA](assets/streaming-media-edge.png)

## Métodos de implementación solo de Adobe Analytics

Los métodos de implementación de Edge descritos anteriormente se recomiendan tanto para Customer Journey Analytics como para Adobe Analytics, especialmente para las nuevas implementaciones.

Además de los métodos de implementación de Edge, hay otros métodos de implementación disponibles. Estos métodos de implementación se diseñaron para su uso con Adobe Analytics. Sin embargo, los clientes existentes con cualquiera de los siguientes métodos de implementación aún pueden hacer que los datos estén disponibles en Customer Journey Analytics creando una [Conexión de origen de Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=es).

* **Extensión de medios con etiquetas:** la extensión de Adobe Medium Analytics para audio y vídeo proporciona la funcionalidad para agregar la instancia de Media Tracker a un sitio o proyecto con etiquetas habilitadas. Los datos se envían directamente a Adobe Analytics.

  Para obtener información sobre la instalación, configuración e implementación de Media Extension con etiquetas, consulte [Extensión de Adobe Medium Analytics (SDK 3.x) para audio y vídeo](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=es).

* **Media SDK:** Media SDK le permite medir varias plataformas de medios, incluidos sitios web, teléfonos móviles, televisores conectados, tabletas, dispositivos OTT, descodificadores y consolas de juegos. (Para obtener más información, consulte [Dispositivos y plataformas compatibles](/help/getting-started/supported-devices.md).)

  Los Media SDK utilizan la API de recopilación de medios para el seguimiento. Los datos se envían directamente a Adobe Analytics.

  Para obtener información sobre la descarga e instalación de Media SDK y extensiones, consulte [Obtención de Media SDK, Extensiones mediante etiquetas y SDK para OTT](/help/getting-started/download-sdks.md).

* **API de colección de medios:** puesto que las API de colección de medios se pueden personalizar, se pueden utilizar para aplicaciones que requieren funcionalidades de seguimiento personalizadas y para dispositivos no compatibles con Media SDK. Las API de colección de medios rastrean los eventos de audio y vídeo mediante llamadas HTTP RESTful. Los datos se envían directamente a Adobe Analytics.

  Para obtener información sobre el uso de las API de recopilación de medios, consulte [API de recopilación de medios](media-collection-api/mc-api-overview.md).


![Flujo de trabajo de Analytics](assets/analytics-implementation.png)

<!--
(Not sure if we need the following paragraph and graphic. Paragraph is somewhat redundant with the intro paragraph of this article)
Choose the implementation method depending on the supported platforms. Some players are not supported by the Media SDKs or the Adobe Experience Platform Media Extensions. The Media Collection APIs provide a way to support those players. For information on supported devices, see [Supported devices and platforms](/help/getting-started/supported-devices.md).

![Media Flow](media-sdk/assets/choose-media-flow2.png)
-->
