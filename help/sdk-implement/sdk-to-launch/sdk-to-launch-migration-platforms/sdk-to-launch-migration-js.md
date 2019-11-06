---
seo-title: Migración del SDK de medios independiente a Adobe Launch - Web (JS)
title: Migración del SDK de medios independiente a Adobe Launch - Web (JS)
seo-description: Instrucciones y ejemplos de código para ayudarle a migrar del SDK de medios a Launch.
description: Instrucciones y ejemplos de código para ayudarle a migrar del SDK de medios a Launch.
translation-type: tm+mt
source-git-commit: b479f6623566b6a6989f625b757a97bba5f6aafd

---


# Migración del SDK de medios independiente a Adobe Launch - Web (JS)

## Diferencias de características

* *Launch* : Launch le proporciona una interfaz de usuario que le guiará a través de la configuración, la configuración y la implementación de sus soluciones de seguimiento de medios basadas en la web. Launch mejora la administración dinámica de etiquetas (DTM).
* *SDK* de medios: El SDK de medios le proporciona bibliotecas de seguimiento de medios diseñadas para plataformas específicas (por ejemplo: Android, iOS, etc.). Adobe recomienda el SDK de medios para rastrear el uso de medios en sus aplicaciones móviles.

## Configuración

### Iniciar extensión

1. En Inicio de plataforma de experiencia, haga clic en la ficha [!UICONTROL Extensiones] de la propiedad web.
1. En la ficha [!UICONTROL Catálogo] , ubique la extensión Adobe Media Analytics para audio y vídeo y haga clic en [!UICONTROL Instalar].
1. En la página de configuración de la extensión, configure los parámetros de seguimiento.
La extensión Media utilizará los parámetros configurados para el seguimiento.

[Guía del usuario de Launch: Instalar y configurar la extensión de medios](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html#install-and-configure-the-ma-extension)

### SDK de medios independiente

En el SDK de medios independiente, puede configurar la configuración de seguimiento en la aplicación y pasarla al SDK cuando cree el rastreador.

```javascript
//Media Heartbeat initialization
var mediaConfig = new MediaHeartbeatConfig();
mediaConfig.trackingServer = "namespace.hb.omtrdc.net";
mediaConfig.playerName = "html5-player";
mediaConfig.channel = "sample-channe";
mediaConfig.ovp = "video-provider";
mediaConfig.appVersion = "v2.0.0"
mediaConfig.ssl = true;
mediaConfig.debugLogging = true;
```

Además de la `MediaHeartbeat` configuración, la página debe configurar y pasar la `AppMeasurement` instancia y la `VisitorAPI` instancia para el seguimiento de medios a fin de que funcionen correctamente.

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
Pase un objeto delegado a `get-instance` que exponga `getQoSObject()` y `getCurrentPlaybackTime()` funciones.

   ```
   var getMediaHeartbeatInstance =
   turbine.getSharedModule('adobe-video-analytics', 'get-instance');
   ```

   Acceda a `MediaHeartbeat` constantes mediante el módulo `media-heartbeat` compartido.

### Media SDK

1. Agregue la biblioteca de Media Analytics al proyecto de desarrollo.
1. Cree un objeto config (`MediaHeartbeatConfig`).
1. Implementar el protocolo delegado, exponiendo las `getQoSObject()` funciones y `getCurrentPlaybackTime()` .
1. Crear una instancia de Media Heartbeat (`MediaHeartbeat`).

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

[SDK de medios - Creación de rastreadores](https://docs.adobe.com/content/help/en/media-analytics/using/sdk-implement/cookbook/sdk-vs-launch-qoe.html)

## Documentación relacionada

### Launch

* [Información general sobre el lanzamiento](https://docs.adobe.com/content/help/en/launch/using/overview.html)
* [Media Analytics Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/media-analytics-extension/overview.html)

### Media SDK

* [Configurar JS](/help/sdk-implement/setup/set-up-js.md)
* [API de JS de Media SDK](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html)

