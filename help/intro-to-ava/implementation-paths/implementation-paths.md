---
title: ¿Qué rutas de implementación de medios de flujo continuo están disponibles?
description: Obtenga información acerca de las rutas de implementación de medios de flujo continuo de Adobe, incluido Adobe Launch.
exl-id: eee70e62-ba45-440a-8ce1-e151b66d2c1f
source-git-commit: 0d5edcae0a80357247ada7f61daece9840d5c4b5
workflow-type: ht
source-wordcount: '499'
ht-degree: 100%

---

# Rutas de implementación {#implementation-paths}

Con cada ruta de implementación, los clientes deberán ponerse en contacto con su representante de ventas/administrador de cuentas para firmar un nuevo pedido de ventas, ya que Media Analytics tiene una SKU única y cambia de un modelo de precios basado en las llamadas del servidor a un modelo basado en las transmisiones de vídeo.

* **Adobe Launch con la extensión de Adobe Media Analytics**

   Adobe Launch es la función de administración de etiquetas de próxima generación de Adobe. Launch ofrece una alternativa sencilla para implementar y gestionar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente. Para crear y mantener sus propias integraciones con Launch, utiliza extensiones. Una extensión es un paquete de JavaScript, HTML y CSS que amplía la funcionalidad del cliente y la interfaz de usuario de Launch. Para obtener más información, consulte la [Guía del usuario de Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/overview.html)

   La extensión de Adobe Media Analytics (MA) agrega el SDK principal de JavaScript Media (Media SDK 2.x) para audio y vídeo. Esta extensión proporciona la funcionalidad para agregar la instancia de seguimiento `MediaHeartbeat` a un sitio o proyecto de Launch.

   Adobe Launch con la extensión Media Analytics requiere lo siguiente:
   * Debe ser cliente de Adobe Experience Cloud.
   * Debe implementar el código incrustado de Launch o DTM en las páginas web.
   * [Extensión de Analytics](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html?lang=es)
   * [Extensión de Experience Cloud ID](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html?lang=es)


* **Lado del cliente:** Son integraciones para Media Analytics únicamente. Puede elegir el SDK de Video Heartbeat o las integraciones de la API de Media Collection (recopilación de medios). Esta ruta se puede utilizar en cualquier reproductor de vídeo, incluidos los reproductores de cliente u OVP como Brightcove, Ooyala, thePlatform, etc.

   Si Media Analytics es la ruta deseada, consulte [Implementación de Media SDK](/help/sdk-implement/setup/setup-overview.md) y [API de recopilación de contenidos.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Para usar Media Analytics, los clientes también deben contar con Adobe Analytics.

* **Adobe Primetime:** Se trata de una solución de Adobe Experience Cloud que ayuda a los programadores y distribuidores de contenido a monetizar el contenido en todos los dispositivos conectados.

   Primetime elimina la complejidad de alcanzar, monetizar y activar audiencias globales en varios dispositivos al proporcionar una plataforma modular para la publicación, publicidad, personalización y análisis de vídeo. Además, Primetime incluye soluciones y valores para lo siguiente:

   * Medir con precisión los tipos de contenido Lineal y VOD.
   * Compatibilidad para medir saltos de anuncios con (o sin) inserción de publicidad dinámica.
   * El modelo de inserción de anuncios optimizado de TVSDK permite realizar análisis que miden directamente la reproducción del anuncio, lo que aumenta la precisión.
   * Conjunto sólido de eventos y metadatos para garantizar la precisión en los problemas de interrupción de la conectividad móvil o de almacenamiento en búfer de QoS y en las interacciones del usuario final, como la búsqueda, la pausa y la puesta en segundo plano en dispositivos móviles.

<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK ya se ha integrado con el SDK de Media Analytics (Heartbeats), que hace que la implementación sea más fácil y rápida en todas las plataformas compatibles. <!--Primetime also supports the partnership with Nielsen.--> Para aprovechar Primetime, siga las mismas directrices y requisitos previos que se encuentran en el [lado del cliente](/help/intro-to-ava/implementation-paths/client-side-path.md), junto con los siguientes documentos para las plataformas: [Guía del usuario de Primetime.](https://helpx.adobe.com/es/support/primetime.html)

También debe ponerse en contacto con el representante de ventas/administrador de cuentas para analizar lo que necesita hacer para comprar TVSDK.
