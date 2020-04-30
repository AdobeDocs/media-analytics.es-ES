---
title: Rutas de implementación
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Rutas de implementación {#implementation-paths}

Media Analytics (Heartbeats) es la solución de vídeo estandarizada de Adobe. Ha reemplazado el modelo anterior de Milestone de Adobe.

Con cada una de estas rutas de implementación, los clientes deberán ponerse en contacto con su representante de ventas/administrador de cuentas para firmar un nuevo pedido de ventas, ya que Media Analytics tiene un SKU único y cambia de un modelo de precios basado en las llamadas del servidor a un modelo basado en las emisiones de vídeo:

* **Lado del cliente:** Son integraciones para Media Analytics únicamente. Puede elegir el SDK de Video Heartbeat o las integraciones de la API de Media Collection (recopilación de medios). Esta ruta se puede utilizar en cualquier reproductor de vídeo, incluidos los reproductores de cliente u OVP como Brightcove, Ooyala, thePlatform, etc.

   Si Media Analytics es la ruta deseada, consulte [Implementación de Media SDK](/help/sdk-implement/setup/setup-overview.md) y [API de recopilación de contenidos.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Para usar Media Analytics, los clientes también deben contar con Adobe Analytics.

* **Adobe Experience Platform Launch:** Adobe Experience Platform Launch, el producto de seguimiento de Dynamic Tag Management, cuenta con una extensión de Media Analytics Launch que facilita la implementación del seguimiento de vídeo en los reproductores.

   Puede obtener más información sobre Experience Platform Launch aquí: [Adobe Media Analytics para la extensión de audio y vídeo](https://docs.adobe.com/content/help/es-ES/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
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
