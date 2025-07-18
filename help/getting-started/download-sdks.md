---
title: Vínculos de acceso para descargar los SDK de Media Analytics
description: Vínculos a las descargas de SDK para plataformas disponibles, como Android, iOS, JavaScript, Chromecast y Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 81%

---

# Obtener SDK de medios, extensiones mediante etiquetas y SDK para OTT {#download-sdks}

La información de esta página incluye vínculos para descargar los SDK de medios actuales y para obtener las extensiones de medios que utilizan etiquetas.

Las etiquetas en Adobe Experience Platform son la nueva generación de capacidades de administración de etiquetas de sitios web y SDK para móviles de Adobe. Las etiquetas ofrecen una alternativa sencilla para implementar y gestionar las soluciones de análisis, marketing y publicidad necesarias para potenciar las experiencias más importantes del cliente. Para obtener información adicional sobre las etiquetas, consulte [Información general sobre etiquetas](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=es).


>[!NOTE]
>
>Para obtener información sobre la descarga de SDK heredados, consulte [Heredado: descargar SDK](/help/legacy/legacy-download-sdks.md).<br>
>&#x200B;>Para obtener información importante acerca de la finalización de la compatibilidad, consulte [Preguntas frecuentes sobre el fin de la compatibilidad](/help/additional-resources/end-of-support-faqs.md).

## SDK de medios y bibliotecas móviles {#media-sdks-libraries}

### Implementación web {#download-web-sdk}

| Plataforma compatible | Soluciones compatibles | Método de implementación | Versión |  API   |  Documentación  |  Muestra  |
|:---:|---|---|---|---| ---| ---|
| ![Icono de JavaScript ](assets/javascript-icon.png)</br>**API de JavaScript** | Adobe Analytics | Solo de Analytics | Web: [Media SDK para JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Referencia de la API de JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Instalar Media SDK mediante JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Muestra de Media SDK para JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![Icono de JavaScript ](assets/javascript-icon.png)</br>**API de JavaScript** | Adobe Analytics | Solo de Analytics | Web: extensión de medios |  | [Extensión de Adobe Medium Analytics (3.x SDK) para audio y vídeo: uso de etiquetas (recopilación de datos)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=es) | [Extensión de Adobe Media Analytics (3.x SDK) para audio y vídeo de muestra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |
| </br>**Web** | Adobe Analytics<p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | Web: Experience Platform Edge |  | [Implementar la colección de medios de streaming mediante Edge Network](/help/implementation/edge/implementation-edge.md) <p>y</p><p>[Enviar datos web a Edge con Adobe Experience Platform Web SDK](/help/implementation/edge/edge-web-sdk.md)</p> | |

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
| ![Icono de Chromecast ](assets/chromecast-icon.png)</br>**Chromecast** | Adobe Analytics | Solo de Analytics | [SDK para Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Referencia de la API de Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Configuración del SDK móvil v3.x para Chromecast](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Icono de Roku ](assets/roku-icon.png)</br>**Roku** | Adobe Analytics | Solo de Analytics | [SDK para Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) |  | [Configuración del SDK móvil v2.x para Roku](/help/implementation/media-sdk/setup/set-up-roku.md) |
| ![Icono de Roku ](assets/roku-icon.png)</br>**Roku** | <p>Adobe Analytics</p><p>Customer Journey Analytics</p><p>Adobe Journey Optimizer</p><p>Real-Time CDP</p> | Edge | [Adobe Experience Platform Roku SDK](https://github.com/adobe/aepsdk-roku/tree/main) |  | [Instalar Media SDK mediante JavaScript](/help/implementation/edge/implementation-edge.md) |
