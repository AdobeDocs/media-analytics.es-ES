---
title: Introducción
description: Introducción a Adobe Analytics Streaming Media.
uuid: null
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: 660aa29a-2a3d-4a4f-acd6-471551d1047b
source-git-commit: 8b939da2374acb5d573a553c848ba880345e64b5
workflow-type: ht
source-wordcount: '439'
ht-degree: 100%

---

# Introducción {#getting-started}

Adobe Analytics para medios de streaming ofrece dos métodos de implementación principales: Media SDK y API de recopilación de medios.

![métodos](assets/getting-started2.png)

Mediante la lógica integrada de los **Media SDK**, puede medir con precisión varias plataformas de medios, incluidos sitios web, teléfonos móviles, televisores conectados, tabletas, dispositivos OTT, decodificadores y consolas de juegos. Incluso puede medir el contenido descargado. La perspectiva que obtiene profundiza en la participación de la visualización de los usuarios, para que pueda comprender cuánto tiempo, cuándo y dónde interactúan. Los Media SDK utilizan la **API de recopilación de medios** para el seguimiento. Las API de recopilación de medios se pueden personalizar, si la aplicación requiere funcionalidades de seguimiento propias. En el caso de dispositivos no compatibles con los Media SDK, puede emplear las API de recopilación de medios.

La solución Adobe Analytics Streaming Media se proporciona para las siguientes plataformas de medios:

* Web
* Móvil
* OTT
* Cualquier dispositivo conectado que se pueda usar para medios de streaming o una integración servidor a servidor

Para obtener más información, consulte [Dispositivos y plataformas compatibles](#_Supported_devices_and).

>[!IMPORTANT]
>
>Para implementar Adobe Analytics Streaming Media, póngase en contacto con su representante de ventas o administrador de cuentas de Adobe para asegurarse de que forme parte de su catálogo de productos.

## Media SDK para medios de streaming {#media-sdks}

Los SDK de medios para medios de streaming están disponibles para las plataformas JavaScript, Android, iOS, tvOS, Chromecast y Roku.

Para obtener información acerca de cómo descargar e instalar Media SDK, consulte [Obtención de Media SDK, extensiones mediante etiquetas y SDK para OTT](/help/getting-started/download-sdks.md).


## API de recopilación de medios {#media-collection-apis}

Las **API de recopilación de medios** le permiten personalizar su implementación de análisis de medios. Utilice las API de recopilación de medios para llamar directamente a los servidores de Adobe y hacer casi cualquier acción que pueda ejecutar con los SDK y más. Personalice la recopilación de datos para crear informes que exploren, obtengan perspectivas o respondan a preguntas importantes acerca de los datos de medios de streaming.

Para obtener información acerca del uso de las API de recopilación de medios, consulte [Documentación de API de medios de streaming](/help/implementation/media-collection-api/mc-api-overview.md).

## Extensiones de Adobe {#adobe-extensions}

* La [**Extensión de Adobe Media Analytics para Audio y Video**](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/media-analytics/overview.html?lang=es) (extensión de Media Analytics) es necesaria para implementaciones de iOS y tvOS. Proporciona la funcionalidad para agregar la instancia de seguimiento a un sitio o proyecto de etiquetas. La extensión MA también requiere la extensión de Analytics y la extensión de ID de Experience Cloud.

* [Extensión de Analytics v1.6 o superior](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=es): esta extensión le permite cargar la biblioteca JavaScript del SDK web de Adobe Experience Platform para enviar datos a las soluciones de Adobe.

* [Extensión de ID de Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=es): esta extensión implementa el servicio de ID de Experience Cloud que identifica a los visitantes en todas las soluciones de Experience Cloud. El servicio de ID de Experience Cloud es una extensión de personalización en Adobe Experience Platform.
