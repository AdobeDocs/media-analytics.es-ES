---
title: ¿Qué rutas de implementación de medios de flujo continuo están disponibles?
description: Obtenga información sobre las rutas de implementación de Adobe Streaming Media, incluida la recopilación de datos de Adobe Experience Platform.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: f88e8b02bc9723793822fa7647a2ceab9ada45e6
workflow-type: ht
source-wordcount: '640'
ht-degree: 100%

---

# Rutas de implementación {#implementation-paths}

Con cada ruta de implementación, los clientes deberán ponerse en contacto con su representante de ventas/administrador de cuentas para firmar un nuevo pedido de ventas, ya que Streaming Media Analytics tiene una SKU única y cambia de un modelo de precios según las llamadas del servidor a un modelo según las transmisiones de vídeo.

## Recopilación de datos de Adobe Experience Platform con la extensión de Adobe Media Analytics

>[!NOTE]
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=es) para obtener una referencia consolidada de los cambios terminológicos.


Las etiquetas de Adobe Experience Platform son la próxima generación de funcionalidades de administración de etiquetas de Adobe. Las etiquetas ofrecen a los clientes una alternativa sencilla para implementar y administrar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente. Las etiquetas se proporcionan a los clientes de Adobe Experience Cloud como una función incluida que añade valor.

Las etiquetas ofrecen a los usuarios las herramientas necesarias para desarrollar y mantener sus propias integraciones, que se denominan extensiones. Estas extensiones están disponibles para los clientes de Adobe Experience Cloud en las tiendas de aplicaciones para que puedan instalar, configurar e implementar rápidamente sus etiquetas.

Una extensión es un paquete de código (JavaScript, HTML y CSS) que amplía la funcionalidad de las etiquetas. Cree, gestione y actualice sus integraciones con una interfaz de autoservicio virtual. Puede considerar las extensiones como aplicaciones que utiliza para realizar sus tareas. Para obtener más información, consulte la *Información general sobre etiquetas* en la [Documentación de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=es)

La extensión de Adobe Media Analytics (MA) agrega el SDK principal de JavaScript Media (Media SDK 2.x) para audio y vídeo. Esta extensión proporciona la funcionalidad para agregar la instancia de seguimiento `MediaHeartbeat` a un sitio o proyecto de recopilación de datos.

La recopilación de datos de Adobe con la extensión Media Analytics requiere lo siguiente:
* Debe ser cliente de Adobe Experience Cloud.
* Debe implementar el código incrustado de la recopilación de datos o DTM en las páginas web.
* [Extensión de Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=es)
* [Extensión de Experience Cloud ID](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/id-service/overview.html?lang=es)


## Lado del cliente

Son integraciones solo de Media Analytics. Puede elegir el SDK de Video Heartbeat o las integraciones de la API de Media Collection (recopilación de medios). Esta ruta se puede utilizar en cualquier reproductor de vídeo, incluidos los reproductores de cliente u OVP como Brightcove, Ooyala, thePlatform, etc.

Si Media Analytics es la ruta deseada, consulte [Implementación de Media SDK](/help/sdk-implement/setup/setup-overview.md) y [API de recopilación de contenidos.](/help/media-collection-api/mc-api-overview.md)

>[!IMPORTANT]
>Para usar Media Analytics, los clientes también deben contar con Adobe Analytics.

## Adobe Primetime

Adobe Primetime es una solución de Adobe Experience Cloud que ayuda a los programadores y distribuidores de contenido a monetizar los medios en todos los dispositivos conectados.

Primetime elimina la complejidad de alcanzar, monetizar y activar audiencias globales en varios dispositivos al proporcionar una plataforma modular para la publicación, publicidad, personalización y análisis de vídeo. Además, Primetime incluye soluciones y valores para lo siguiente:

* Medir con precisión los tipos de contenido Lineal y VOD.
* Compatibilidad para medir saltos de anuncios con (o sin) inserción de publicidad dinámica.
* El modelo de inserción de anuncios optimizado de TVSDK permite realizar análisis que miden directamente la reproducción del anuncio, lo que aumenta la precisión.
* Conjunto sólido de eventos y metadatos para garantizar la precisión en los problemas de interrupción de la conectividad móvil o de almacenamiento en búfer de QoS y en las interacciones del usuario final, como la búsqueda, la pausa y la puesta en segundo plano en dispositivos móviles.
* Compatibilidad integrada de Nielsen DTVR (lineal) con metadatos ID3 y de DCR con metadatos CMS.


TVSDK ya se ha integrado con el SDK de Media Analytics (Heartbeats), que hace que la implementación sea más fácil y rápida en todas las plataformas compatibles. Para aprovechar Primetime, siga las mismas directrices y requisitos previos que se encuentran en el [lado del cliente](/help/intro-to-ava/implementation-paths/client-side-path.md), junto con los siguientes documentos para las plataformas: [Guía del usuario de Primetime.](https://helpx.adobe.com/es/support/primetime.html)

También debe ponerse en contacto con el representante de ventas/administrador de cuentas para analizar lo que necesita hacer para comprar TVSDK.
