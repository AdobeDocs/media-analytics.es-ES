---
title: Implementación de medios de streaming para Adobe Analytics o Customer Journey Analytics
description: Obtenga información acerca de las rutas de implementación de Streaming Media.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
source-git-commit: 984f058fda15b1c5e960e4c8d8e2378308d2b541
workflow-type: ht
source-wordcount: '471'
ht-degree: 100%

---

# Implementación de medios de transmisión para Adobe Analytics o Customer Journey Analytics

Existen varias formas de implementar Streaming Media. Para ver una comparación detallada de los dispositivos y las plataformas compatibles con los métodos de implementación descritos en esta página, consulte [Dispositivos y plataformas compatibles](/help/getting-started/supported-devices.md).

## Métodos de implementación de Edge

Se recomienda utilizar Edge al implementar Media Analytics para todos los clientes nuevos de Adobe Analytics o Customer Journey Analytics.

* **Medios para la extensión/SDK de la red perimetral:** Recopila datos de dispositivos iOS y Android y los envía a Edge. A continuación, los datos se pueden enviar a Customer Journey Analytics o a Adobe Analytics.

  Para obtener más información acerca de la extensión/SDK de Media for Edge Network, consulte [Instalación de Media Analytics con Experience Platform Edge](/help/implementation/edge/implementation-edge.md).

  >[!NOTE]
  >
  >Actualmente, este método de implementación no es compatible con el SDK web o Roku. Sin embargo, ambos son compatibles al implementar con la API de Media Edge.

* **API de Media Edge:** se puede personalizar para recopilar datos de cualquier dispositivo o formato (incluidos dispositivos móviles, web y de servicios OTT) y enviar datos a Edge. A continuación, los datos se pueden enviar a Customer Journey Analytics o a Adobe Analytics.

  <!-- For more information about the Media Edge API, see (link to John's docs when they're ready) -->

![Flujo de trabajo de CJA](assets/cja-implementation.png)

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
