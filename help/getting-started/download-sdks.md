---
title: Vínculos de acceso para descargar los SDK de Media Analytics
description: Vínculos a las descargas de SDK para plataformas disponibles, como Android, iOS, JavaScript, Chromecast y Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/-L2tSDNue-GheYE-krKkpnOh05s5GKZZBz5sFXsBJ3I
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdbid: df312454-73c4-43f6-a90e-18f5043f074c
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 522
ht-degree: 81%

---

# Obtener SDK de medios, extensiones mediante etiquetas y SDK para OTT {#download-sdks}

La información de esta página incluye vínculos para descargar los SDK de medios actuales y para obtener las extensiones de medios que utilizan etiquetas.

Las etiquetas en Adobe Experience Platform son la nueva generación de capacidades de administración de etiquetas de sitios web y SDK para móviles de Adobe. Las etiquetas ofrecen una alternativa sencilla para implementar y gestionar las soluciones de análisis, marketing y publicidad necesarias para potenciar las experiencias más importantes del cliente. Para obtener información adicional sobre las etiquetas, consulte [Información general sobre etiquetas](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=es).

## SDK de medios y bibliotecas móviles {#media-sdks-libraries}

### Implementación web {#download-web-sdk}

| Plataforma compatible | Soluciones compatibles | Método de implementación | Versión |  API   |  Documentación  |  Muestra  |
|:---:|---|---|---|---| ---| ---|
| ![Icono de JavaScript ](assets/javascript-icon.png)</br>**API de JavaScript** | Adobe Analytics | Solo de Analytics | Web: [Media SDK para JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Referencia de la API de JavaScript](/help/implementation/media-sdk/setup/js-3x-api-reference.md) | [Instalar Media SDK mediante JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Muestra de Media SDK para JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![Icono de JavaScript ](assets/javascript-icon.png)</br>**API de JavaScript** | Adobe Analytics | Solo de Analytics | Web: extensión de medios |  | [Extensión de Adobe Medium Analytics (3.x SDK) para audio y vídeo: uso de etiquetas (recopilación de datos)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=es) | [Extensión de Adobe Media Analytics (3.x SDK) para audio y vídeo de muestra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web: Experience Platform Edge |  | [Implementar la colección de medios de streaming de Customer Journey Analytics mediante Edge Network](/help/implementation/edge/implementation-edge.md) <p>y</p><p>[Enviar datos web a Edge con Adobe Experience Platform Web SDK](/help/implementation/edge/edge-web-sdk.md)</p> | |

### Implementación móvil {#get-mobile-extension}

| Plataforma compatible | Soluciones compatibles | Método de implementación | Versión |  Documentación   |  Ejemplos  |
|:---:|---|---|---|---|---|
| ![Icono de Android ](assets/android-icon.png)</br>**Android** | Adobe Analytics | Solo de Analytics | Android: extensión de medios | [Documentación de Mobile SDK](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics: Media Analytics para audio y vídeo de muestra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Icono de Apple iOS ](assets/ios-icon.png)<br>**tvOS** | Adobe Analytics | Solo de Analytics | iOS/tvOS: extensión de medios | [Documentación de Mobile SDK](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/) | [Adobe Analytics: Media Analytics para audio y vídeo de muestra](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |
| ![Icono de Android ](assets/android-icon.png)</br>**Android** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Android: Experience Platform Edge | [Instalar Media SDK mediante JavaScript](/help/implementation/edge/implementation-edge.md) | |
| ![Icono de Apple iOS ](assets/ios-icon.png)<br>**tvOS** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | iOS/tvOS: Experience Platform Edge | [Instalar Media SDK mediante JavaScript](/help/implementation/edge/implementation-edge.md) |  |

### Implementación OTT {#download-ott-libraries}

| Plataforma compatible | Soluciones compatibles | Método de implementación | Versión |  API   |  Documentación  |
|:---:|---|---|---|---|---|
| ![Icono de Chromecast ](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Solo de Analytics | [SDK para Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Referencia de la API de Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Configurar Chromecast SDK](https://github.com/Adobe-Marketing-Cloud/media-sdks/blob/master/docs/2.x/chromecast-setup.md) |
| ![Icono de Roku ](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main) |  | [Instalar Media SDK mediante JavaScript](/help/implementation/edge/implementation-edge.md) |
