---
seo-title: Comprender las diferencias entre Launch y Media SDK
title: Comprender las diferencias entre Launch y Media SDK
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# Comprender las diferencias entre Launch y Media SDK

## Diferencias entre funciones

* *Launch* - Launch le proporciona una interfaz de usuario que le guía por la configuración, configuración e implementación de las soluciones de seguimiento de medios basadas en web. Launch mejora en la administración dinámica de etiquetas (DTM).
* *SDK* multimedia: El SDK multimedia le proporciona bibliotecas de seguimiento de medios diseñadas para plataformas específicas (p. ej.: Android, iOS, etc.). Adobe recomienda el SDK de medios para rastrear el uso de medios en sus aplicaciones móviles.

## Diferencias de creación del rastreador

### Launch

Launch ofrece dos métodos para crear la infraestructura de seguimiento. Ambos métodos utilizan la extensión Launch de Media Analytics:

1. Use las API de seguimiento de medios desde una página web.

   En este escenario, Media Analytics Extension exporta las API de seguimiento de medios a una variable configurada en el objeto de ventana global:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Use las API de seguimiento de medios desde otra extensión de inicio.

   En este escenario, utiliza las API de seguimiento de medios expuestas por `get-instance` los módulos `media-heartbeat` y los módulos compartidos.

   >[!NOTE]
   >
   >Los módulos compartidos no están disponibles para su uso en páginas web. Solo puede utilizar módulos compartidos desde otra extensión.

   Cree `MediaHeartbeat` una instancia usando el Módulo `get-instance` compartido.
Transfiera un objeto delegado a `get-instance` los detalles `getQoSObject()` y `getCurrentPlaybackTime()` funciones.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Las `MediaHeartbeat` constantes de acceso a través del `media-heartbeat` Módulo compartido.

### Media SDK

1. Agregue la biblioteca de Media Analytics a su proyecto de desarrollo.
1. Cree un objeto de configuración (`MediaHeartbeatConfig`).
1. Implemente el protocolo delegado, exponer las `getQoSObject()` funciones y las `getCurrentPlaybackTime()` funciones.
1. Cree una instancia de Media Heartbeat (`MediaHeartbeat`).

```
// Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
...
// Configuration settings
mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER;
...
// Implement Media Delegate (Quality of Service and Playhead)
var mediaDelegate = new MediaHeartbeatDelegate();
...
mediaDelegate.getQoSObject = function() {
    return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>);
    ...
}
...
// Create your tracker
this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
```

## Documentación relacionada

### Launch

* [Información general sobre Launch](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [MA Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Media SDK

* [Configurar JS](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

