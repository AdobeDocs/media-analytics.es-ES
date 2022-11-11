---
title: Introducción
description: Introducción a Adobe Analytics para medios de transmisión.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 6%

---


# Introducción {#getting-started}

Adobe Analytics para medios de transmisión ofrece dos métodos de implementación principales: Media SDK y las API de recopilación de contenido.

![métodos](assets/getting-started2.png)

Uso de la lógica integrada de la variable **Media SDK**, puede medir con precisión varias plataformas de medios, incluidos sitios web, teléfonos móviles, televisores conectados, tabletas, dispositivos OTT, decodificadores y consolas de juegos. Incluso puede medir el contenido descargado. La perspectiva que obtiene profundiza en la participación de la visualización de usuarios, para que pueda comprender cuánto tiempo, cuándo y dónde interactúan los visualizadores. Los Media SDK utilizan la variable **API de recopilación de medios** para seguimiento. Las API de recopilación de medios se pueden personalizar si la aplicación requiere capacidades de seguimiento personalizadas. En el caso de dispositivos no compatibles con los Media SDK, puede utilizar las API de Media Collection.

La solución Adobe Analytics Streaming Media se proporciona para las siguientes plataformas de medios:

* Web
* Móvil
* Sobre-arriba
* Cualquier dispositivo conectado que se pueda utilizar para la transmisión por secuencias o una integración servidor a servidor

Para obtener más información, consulte [Dispositivos y plataformas compatibles](#_Supported_devices_and).

>[!IMPORTANT]
>
>Para implementar Adobe Analytics Streaming Media, póngase en contacto con su representante de ventas de Adobe o con el administrador de cuentas para asegurarse de que Streaming Media forme parte de su portafolio de productos.

## Media SDK para medios de transmisión {#media-sdks}

Los SDK de medios para medios de transmisión están disponibles para las plataformas JavaScript, Android, iOS, tvOS, Chromecast y Roku.

Para obtener información sobre cómo descargar e instalar Media SDK, consulte [Obtención de Media SDK, extensiones mediante etiquetas y SDK para OTT](/help/getting-started/download-sdks.md).


## API de recopilación de medios {#media-collection-apis}

La variable **API de recopilación de medios** le permite personalizar su implementación de media analytics. Utilice las API de Media Collection para llamar directamente a los servidores de Adobe y realizar casi cualquier acción que pueda realizar con los SDK y más. Personalice la recopilación de datos para crear informes que exploren, obtengan perspectivas o respondan a preguntas importantes sobre los datos de transmisión por secuencias.

Para obtener información sobre el uso de las API de recopilación de medios, consulte [Documentación de la API de medios de transmisión](/help/implementation/media-collection-api/mc-api-overview.md).

## Extensiones de Adobe {#adobe-extensions}

>[!NOTE]
>
>NECESITA INTRODUCCIÓN PARA LAS EXTENSIONES

* La variable [**Extensión de Adobe Medium Analytics for Audio and Video**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=en) (Extensión de Media Analytics), es necesario para implementaciones de iOS y tvOS. Proporciona la funcionalidad para agregar la instancia de seguimiento a un sitio o proyecto de etiquetas. La extensión MA también requiere la extensión de Analytics y la extensión de ID de Experience Cloud.

* [Extensión de Analytics v1.6 o superior](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=en): Esta extensión le permite cargar la biblioteca JavaScript del SDK web de Adobe Experience Platform para enviar datos a las soluciones de Adobe.

* [Extensión de ID de Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=en): Esta extensión implementa el servicio de ID de Experience Cloud que identifica a los visitantes en todas las soluciones de Experience Cloud. El servicio de ID de Experience Cloud es una extensión de personalización en Adobe Experience Platform.
