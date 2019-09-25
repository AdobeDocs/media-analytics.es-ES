---
seo-title: Understand Launch versus Media SDK differences
title: Understand Launch versus Media SDK differences
uuid: null
translation-type: tm+mt
source-git-commit: 932af09a0692ef35ab46fb6f34b2dec5f2e1e562

---


# Understand Launch versus Media SDK differences

## Diferencias de características

* *Launch* : Launch le proporciona una interfaz de usuario que le guiará a través de la configuración, la configuración y la implementación de sus soluciones de seguimiento de medios basadas en la web. Launch mejora la administración dinámica de etiquetas (DTM).
* *SDK* de medios: El SDK de medios le proporciona bibliotecas de seguimiento de medios diseñadas para plataformas específicas (por ejemplo: Android, iOS, etc.). Adobe recomienda el SDK de medios para rastrear el uso de medios en sus aplicaciones móviles.

## Diferencias en la creación del rastreador

### Launch

Launch ofrece dos métodos para crear la infraestructura de seguimiento. Ambos métodos utilizan la extensión de inicio de Media Analytics:

1. Utilice las API de seguimiento de medios de una página web.

   En este escenario, Media Analytics Extension exporta las API de seguimiento de medios a una variable configurada en el objeto de ventana global:

   ```
   window["CONFIGURED_VARIABLE_NAME"].MediaHeartbeat.getInstance
   ```

1. Utilice las API de seguimiento de medios de otra extensión de Launch.

   En este escenario, se utilizan las API de seguimiento de medios expuestas por los módulos `get-instance` y `media-heartbeat` compartidos.

   >[!NOTE]
   >
   >Los módulos compartidos no están disponibles para su uso en páginas web. Sólo puede usar módulos compartidos desde otra extensión.

   Cree una `MediaHeartbeat` instancia mediante el módulo `get-instance` compartido.
Pass a delegate object to  that exposes  and  functions.`get-instance``getQoSObject()``getCurrentPlaybackTime()`

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Acceda a `MediaHeartbeat` constantes mediante el módulo `media-heartbeat` compartido.

### Media SDK

1. Add the Media Analytics library to your development project.
1. Create a config object ().`MediaHeartbeatConfig`
1. Implementar el protocolo delegado, exponiendo las `getQoSObject()` funciones y `getCurrentPlaybackTime()` .
1. Create a Media Heartbeat instance ().`MediaHeartbeat`

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

* [Información general sobre el lanzamiento](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Extensión de MA](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Media SDK

* [Set up JS](/help/sdk-implement/setup/set-up-js.md)
* [API](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

