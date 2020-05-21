---
title: Rutas de implementación
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: 0bc3928b8e3076feb8e9a16e005cd0415f723408
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 64%

---


# Rutas de implementación {#implementation-paths}

Para cada ruta de implementación, los clientes deben ponerse en contacto con su representante de ventas/administrador de cuentas para firmar un nuevo pedido de venta, ya que Media Analytics tiene un SKU único y cambia de un modelo de precios basado en llamadas al servidor a un modelo basado en flujos de vídeo.

* **Adobe Launch con la extensión Adobe Media Analytics**

   Adobe Launch es la solución de administración de etiquetas de próxima generación de Adobe. Launch proporciona una manera sencilla de implementar y administrar todas las etiquetas de análisis, marketing y publicidad necesarias para potenciar las experiencias relevantes de los clientes. Para crear y mantener sus propias integraciones con Launch, utilice extensiones. Una extensión es un paquete JavaScript, HTML y CSS que amplía la interfaz de usuario de Launch y la funcionalidad del cliente. Para obtener más información, consulte la Guía del usuario del [Experience Platform Launch](https://docs.adobe.com/content/help/es-ES/launch/using/overview.html)

   La extensión Adobe Media Analytics (MA) agrega el SDK principal de medios JavaScript (SDK de Media 2.x) para audio y vídeo. Esta extensión proporciona la funcionalidad para agregar la instancia de seguimiento `MediaHeartbeat` a un sitio o proyecto de Launch.

   Adobe Launch con la extensión Media Analytics requiere lo siguiente:
   * Debe ser cliente de Adobe Experience Cloud.
   * Debe implementar el código incrustado de Launch o DTM en las páginas web.
   * [Extensión de Analytics](https://docs.adobe.com/content/help/es-ES/launch/using/extensions-ref/adobe-extension/analytics-extension/overview.html)
   * [Extensión de Experience Cloud ID](https://docs.adobe.com/content/help/es-ES/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html)


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
