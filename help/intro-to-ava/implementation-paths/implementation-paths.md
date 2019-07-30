---
seo-title: Rutas de implementación
title: Rutas de implementación
uuid: 8400 c 938-e 77 e -4 c 88-b 23 b -5 f 5977 a 5316 c
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Rutas de implementación {#implementation-paths}

Media Analytics (Latidos) es la solución de vídeo estandarizada de Adobe. Ha reemplazado el modelo anterior de Milestone de Adobe.

Para cada una de estas rutas de implementación, los clientes deben ponerse en contacto con el representante de ventas/Administrador de cuentas para firmar un nuevo pedido de ventas, ya que Media Analytics tiene un SKU único y cambios de un modelo de precios según las llamadas del servidor a un modelo basado en flujos de video:

* **Cliente: son** integraciones solo de Media Analytics. Puede elegir entre las integraciones del SDK de Video Heartbeat o la API de Media Collection. Esta ruta se puede utilizar en cualquier reproductor de vídeo, incluidos los reproductores de cliente u OVP como Brightcove, Ooyala, thePlatform, etc.

   If Media Analytics is your intended path, see the [Media SDK Implementation](/help/sdk-implement/setup/setup-overview.md) and the [Media Collection API.](/help/media-collection-api/mc-api-overview.md)

   >[!IMPORTANT]
   >
   >Para utilizar Media Analytics, los clientes también deben utilizar Adobe Analytics.

* **Lanzamiento de Plataforma de Adobe Experience:** Launch de Adobe Experience Platform, el producto que sigue a Administración dinámica de etiquetas, incluye una extensión de inicio de Media Analytics que facilita la implementación del seguimiento de vídeo en sus reproductores.

   You can learn more about Experience Platform Launch here: [Adobe Media Analytics for Audio and Video Extension](https://docs.adobelaunch.com/extension-reference/web/adobe-media-analytics-for-audio-and-video-extension)
* **Adobe Primetime:** Adobe Primetime es una solución de Adobe Experience Cloud que ayuda a programadores y distribuidores de contenido a monetizar medios en todas las pantallas conectadas.

   Primetime elimina la complejidad de alcanzar, monetizar y activar las audiencias globales en diversos dispositivos, proporcionando una plataforma modular para publicación, publicidad, personalización y análisis de vídeo. Además, Primetime ofrece soluciones y valores para lo siguiente:

   * Compatibilidad con la medición precisa de tipos de contenido en formato Linear y VOD.
   * Compatibilidad con la medición de cortes de publicidad con (o sin) inserción dinámica de publicidad.
   * El modelo de inserción de anuncios ininterrumpido de TVSDK permite un análisis que mide directamente la reproducción de la publicidad, lo que aumenta la precisión.
   * Un sólido conjunto de eventos y metadatos para garantizar la precisión entre el almacenamiento en búfer de la calidad del programa o los problemas de las interrupciones de conectividad móvil o con las interacciones con el usuario final, como la búsqueda, la pausa y la comprobación de antecedentes en dispositivos móviles.
   * Compatibilidad integrada de Nielsen DTVR (lineal) con metadatos ID3 y de DCR con metadatos CMS.
   TVSDK ya se ha integrado con el SDK de Medios de medios (Heartbeat), lo que facilita y acelera la implementación en todas las plataformas admitidas. Primetime también admite la asociación en Nielsen. Para aprovechar las Primetime, siga las mismas pautas y requisitos previos que se encuentran en [Lado del cliente](/help/intro-to-ava/implementation-paths/client-side-path.md) junto con los siguientes documentos para su plataforma: [Guía del usuario Primetime.](https://helpx.adobe.com/primetime/user-guide.html)

   También debe ponerse en contacto con el representante de ventas/administrador de cuentas para analizar lo que necesita hacer para comprar TVSDK.
