---
title: Implementación de servicios de medios de streaming para Adobe Analytics o Customer Journey Analytics
description: Obtenga información acerca de las rutas de implementación para los servicios de medios de streaming de Adobe.
uuid: null
feature: Streaming Media
role: User, Admin, Developer
exl-id: ed9297b1-6487-4099-bc62-0c3a40572255
TQID: https://experienceleague.adobe.com/aFrxbzBLlf1ngetaM-GsNFXz6TUXi6Pic3quLVI297c
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
    internal-label: Implementations
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
    internal-label: Media Analytics
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
    internal-label: Methods
  - id: df312454-73c4-43f6-a90e-18f5043f074c
    internal-label: Tags
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 1a499f8948bb649bb61df42e4056ac869e04faa9
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 65%
---
# Implementación de servicios de medios de streaming para Adobe Analytics o Customer Journey Analytics

Existen varias formas de implementar los servicios de medios de streaming de Adobe. Para ver una comparación detallada de los dispositivos y las plataformas compatibles con los métodos de implementación descritos en esta página, consulte [Dispositivos y plataformas compatibles](/help/getting-started/supported-devices.md).

## Métodos de implementación de Edge

Adobe recomienda utilizar métodos de implementación de Edge Network para todos los clientes nuevos de Adobe Analytics o Customer Journey Analytics.

* **Medios para Edge Network SDK / Extensión:** Recopila datos de la web, dispositivos iOS y Android o dispositivos Roku y los envía a Edge Network. A continuación, los datos se pueden enviar a Customer Journey Analytics o a Adobe Analytics.

  Para obtener más información acerca de Media for Edge Network SDK / Extension, consulte [Descripción general de la implementación de Edge](/help/implementation/edge/overview.md).

* **API de Media Edge:** se puede personalizar para recopilar datos de cualquier dispositivo o formato (incluidos dispositivos móviles, web y de servicios OTT) y enviar datos a Edge Network. A continuación, los datos se pueden enviar a Customer Journey Analytics o a Adobe Analytics.

  Para obtener más información sobre la API de Media Edge, consulte [Información general sobre la API de Media Edge](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/).

![Flujo de trabajo de CJA](assets/streaming-media-edge.png)

## Métodos de implementación solo de Adobe Analytics

Los métodos de implementación de Edge descritos anteriormente se recomiendan tanto para Customer Journey Analytics como para Adobe Analytics, especialmente para las nuevas implementaciones.

Además de los métodos de implementación de Edge, hay otros métodos de implementación disponibles. Estos métodos de implementación se diseñaron para su uso con Adobe Analytics. Sin embargo, los clientes existentes con cualquiera de los siguientes métodos de implementación aún pueden hacer que los datos estén disponibles en Customer Journey Analytics creando una [Conexión de origen de Analytics](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/adobe-applications/analytics.html?lang=es).

Los métodos de implementación solo de Adobe Analytics utilizan el complemento de Adobe Analytics para medios de streaming. Para conocer los requisitos previos y una lista de métodos, consulte la [descripción general de la implementación solo de Analytics](/help/implementation/analytics-only/overview.md).

* **Extensión de medios con etiquetas:** la extensión de Adobe Medium Analytics para audio y vídeo proporciona la funcionalidad para agregar la instancia de Media Tracker a un sitio o proyecto con etiquetas habilitadas. Los datos se envían directamente a Adobe Analytics.

  Para obtener información sobre la instalación, configuración e implementación de Media Extension con etiquetas, consulte [Extensión de Adobe Medium Analytics (SDK 3.x) para audio y vídeo](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=es).

* **Media SDK:** Media SDK le permite medir varias plataformas de medios, incluidos sitios web, teléfonos móviles, televisores conectados, tabletas, dispositivos OTT, descodificadores y consolas de juegos. (Para obtener más información, consulte [Dispositivos y plataformas compatibles](/help/getting-started/supported-devices.md).)

  Los Media SDK utilizan la API de recopilación de medios para el seguimiento. Los datos se envían directamente a Adobe Analytics.

  Para obtener información sobre la descarga e instalación de Media SDK y extensiones, consulte [Obtención de Media SDK, Extensiones mediante etiquetas y SDK para OTT](/help/getting-started/download-sdks.md).

* **API de colección de medios:** puesto que las API de colección de medios se pueden personalizar, se pueden utilizar para aplicaciones que requieren funcionalidades de seguimiento personalizadas y para dispositivos no compatibles con Media SDK. Las API de colección de medios rastrean los eventos de audio y vídeo mediante llamadas HTTP RESTful. Los datos se envían directamente a Adobe Analytics.

  Para obtener información sobre el uso de las API de recopilación de medios, consulte [API de recopilación de medios](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/).


![Flujo de trabajo de Analytics](assets/analytics-implementation.png)
