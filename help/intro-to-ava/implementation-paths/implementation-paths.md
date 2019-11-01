---
title: Rutas de implementación
description: null
uuid: 8400c938-e77e-4c88-b23b-5f5977a5316c
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Rutas de implementación {#implementation-paths}

Media Analytics (latidos) es la solución de vídeo estandarizada de Adobe. Ha reemplazado el modelo anterior de Milestone de Adobe.

Para cada una de estas rutas de implementación, los clientes deben ponerse en contacto con su representante de ventas/administrador de cuentas para firmar un nuevo pedido de venta, ya que Media Analytics tiene un SKU único y cambia de un modelo de precios basado en llamadas al servidor a un modelo basado en flujos de vídeo:

* **Lado del cliente:** son integraciones solo de Media Analytics. Puede elegir entre las integraciones del SDK de Video Heartbeat o la API de Media Collection. Esta ruta se puede utilizar en cualquier reproductor de vídeo, incluidos los reproductores de cliente u OVP como Brightcove, Ooyala, thePlatform, etc.

   If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Para utilizar Media Analytics, los clientes también deben utilizar Adobe Analytics.

* **Lanzamiento de la plataforma Adobe Experience** Platform: Adobe Experience Platform Launch, el producto complementario de la administración dinámica de etiquetas, incluye una extensión de inicio de Media Analytics que facilita la implementación del seguimiento de vídeo en los reproductores.

   Puede obtener más información sobre el lanzamiento de la plataforma de experiencia aquí: [Adobe Media Analytics para la extensión de audio y vídeo](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)
* **Adobe Primetime:** Adobe Primetime es una solución de Adobe Experience Cloud que ayuda a los programadores y distribuidores de contenido a monetizar los medios en todas las pantallas conectadas.

   Primetime elimina la complejidad de alcanzar, monetizar y activar las audiencias globales en diversos dispositivos, proporcionando una plataforma modular para publicación, publicidad, personalización y análisis de vídeo. Además, Primetime ofrece soluciones y valores para lo siguiente:

   * Compatibilidad con la medición precisa de tipos de contenido en formato Linear y VOD.
   * Compatibilidad con la medición de cortes de publicidad con (o sin) inserción dinámica de publicidad.
   * El modelo de inserción de anuncios ininterrumpido de TVSDK permite un análisis que mide directamente la reproducción de la publicidad, lo que aumenta la precisión.
   * Un sólido conjunto de eventos y metadatos para garantizar la precisión entre el almacenamiento en búfer de la calidad del programa o los problemas de las interrupciones de conectividad móvil o con las interacciones con el usuario final, como la búsqueda, la pausa y la comprobación de antecedentes en dispositivos móviles.
<!--
   * Integrated support for Nielsen DTVR (linear) with ID3 metadata and DCR with CMS metadata.
-->

TVSDK ya está integrado con el SDK de Media Analytics (latidos), lo que facilita y acelera la implementación en todas las plataformas admitidas. <!--Primetime also supports the partnership with Nielsen.--> Para aprovechar Primetime, siga las mismas directrices y requisitos previos que se encuentran en el [cliente](/help/intro-to-ava/implementation-paths/client-side-path.md) , junto con los siguientes documentos para las plataformas: Guía [del usuario de Primetime.](https://helpx.adobe.com/primetime/user-guide.html)

También debe ponerse en contacto con el representante de ventas/administrador de cuentas para analizar lo que necesita hacer para comprar TVSDK.
