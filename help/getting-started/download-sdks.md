---
title: Vínculos de acceso para descargar los SDK de Media Analytics
description: Vínculos a las descargas de SDK para plataformas disponibles, como Android, iOS, JavaScript, Chromecast y Roku.
uuid: a619fbb8-693e-4583-8dad-0ff875e715f8
exl-id: d211fa2e-d5b0-4e9f-bdb7-eda838194f3d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '645'
ht-degree: 100%

---

# Obtener SDK de medios, extensiones mediante etiquetas y SDK para OTT {#download-sdks}

La información de esta página incluye vínculos para descargar los SDK de medios actuales y obtener las extensiones de medios.

La información de esta página incluye vínculos para descargar los SDK de medios actuales y para obtener las extensiones de medios que utilizan etiquetas.

Las etiquetas en Adobe Experience Platform son la nueva generación de capacidades de administración de etiquetas de sitios web y SDK para móviles de Adobe. Las etiquetas ofrecen una alternativa sencilla para implementar y gestionar las soluciones de análisis, marketing y publicidad necesarias para potenciar las experiencias más importantes del cliente. Para obtener información adicional sobre las etiquetas, consulte [Información general sobre etiquetas](https://experienceleague.adobe.com/docs/platform-learn/data-collection/overview.html?lang=es)


>[!NOTE]
>
>Para obtener información sobre la descarga de SDK heredados, consulte [Heredado: descargar SDK](/help/legacy/legacy-download-sdks.md).<br>
>Para obtener información importante acerca de la finalización de la compatibilidad, consulte [Preguntas frecuentes sobre el fin de la compatibilidad](/help/additional-resources/end-of-support-faqs.md).

## SDK de medios y bibliotecas móviles {#media-sdks-libraries}

### Implementación web {#download-web-sdk}

| Plataforma compatible | Versión |  API   |  Documentación  |  Muestra  |
|:---:|---|---|---|---|
| ![Icono de JavaScript](assets/javascript-icon.png) | Web: [Media SDK para JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/js-v3.0.2) | [Referencia de la API de JavaScript](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) | [Configuración de Media SDK v3.x para JavaScript](/help/implementation/media-sdk/setup/web-implementation.md) | [Muestra de Media SDK para JS v3.0.2](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/sdks/js/3.x) |
| ![Icono de JavaScript](assets/javascript-icon.png) | Web: extensión de medios |  | [Extensión de Adobe Medium Analytics (3.x SDK) para audio y vídeo: uso de etiquetas (recopilación de datos)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics-3x/overview.html?lang=es) | [Extensión de Adobe Media Analytics (3.x SDK) para audio y vídeo de muestra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x) |

### Implementación móvil {#get-mobile-extension}

| Plataforma compatible | Versión |  Documentación   |  Ejemplos  |
|:---:|---|---|---|
| ![Icono de Android](assets/android-icon.png) | Android: extensión de medios | [Documentación de Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics: Media Analytics para audio y vídeo de muestra](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/mobile/android) |
| ![Icono de Apple iOS ](assets/ios-icon.png)<br> agregar icono de tvOS | iOS/tvOS: extensión de medios | [Documentación de Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) | [Adobe Analytics: Media Analytics para audio y vídeo de muestra](https://github.com/adobe/aepsdk-media-ios/tree/main/TestApp) |

### Implementación OTT {#download-ott-libraries}

| Plataforma compatible | Versión |  API   |  Documentación  |
|:---:|---|---|---|
| ![Icono de Chromecast](assets/chromecast-icon.png) | [SDK para Chromecast v3.0.3](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/chromecast-v3.0.3) | [Referencia de la API de Chromecast](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/) | [Configuración del SDK móvil v3.x para Chromecast](/help/implementation/media-sdk/setup/set-up-chromecast.md) |
| ![Icono de Roku](assets/roku-icon.png) | [SDK para Roku v2.2.6](https://github.com/Adobe-Marketing-Cloud/media-sdks/releases/tag/roku-v2.2.6) | [Referencia de la API de Roku](/help/implementation/media-sdk/setup/set-up-roku.md) | [Configuración del SDK móvil v2.x para Roku](/help/implementation/media-sdk/setup/set-up-roku.md) |

## Extensiones de Adobe {#adobe-extensions}

### Extensión de medios de streaming {#streaming-media-extension}

La **Extensión de Adobe Media Analytics para Audio y Video** requiere la unidad de almacén (SKU) del complemento de Adobe Analytics para medios. Para obtener más información, póngase en contacto con su representante de ventas, administrador de cuentas o Customer Success Manager de Adobe.

Para obtener información detallada sobre la instalación, configuración e implementación de la variable **Extensión de Adobe Media Analytics para Audio y Video**, consulte [Información general sobre la extensión de Adobe Media Analytics para Audio y Video](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=es) y [Configuración de la extensión de Media Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics#configure-the-media-analytics-extension).

### Extensión de Analytics {#analytics-extension}

[Extensión de Analytics v1.6 o superior](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=es): esta extensión le permite cargar la biblioteca JavaScript del SDK web de Adobe Experience Platform para enviar datos a las soluciones de Adobe.Se requiere la **Extensión de Analytics** v1.6 o posterior.

Para obtener información acerca de cómo configurar esta extensión, consulte [Configuración de la extensión de Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=es).

### Extensión de Experience Cloud ID {#cloud-id-extension}

[Extensión de ID de Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=es): esta extensión implementa el servicio de ID de Experience Cloud que identifica a los visitantes en todas las soluciones de Experience Cloud. El servicio de ID de Experience Cloud es una extensión de personalización en Adobe Experience Platform.

Utilice esta extensión para integrar Experience Cloud Identity Service con su propiedad. Con Experience Cloud Identity Service, puede crear y almacenar ID únicos y persistentes para los visitantes del sitio.

Para obtener información acerca de cómo configurar esta extensión, consulte [Configuración de la extensión de ID de Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=es)
