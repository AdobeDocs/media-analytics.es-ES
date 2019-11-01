---
title: Configuración de JavaScript
description: Configuración de la aplicación del SDK de medios para la implementación en JavaScript.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Configuración de JavaScript{#set-up-javascript}

## Requisitos previos

* **Obtener parámetros** de configuración válidos Estos parámetros se pueden obtener de un representante de Adobe después de configurar la cuenta de Analytics.
* **Implementar`AppMeasurement`para JavaScript en la aplicación** multimedia. Para obtener más información sobre la documentación de SDK de Adobe Mobile, consulte [Implementación de Analytics con JavaScript.](https://marketing.adobe.com/resources/help/en_US/sc/implement/js_implementation.html)

* **Proporcione las siguientes capacidades en su reproductor de medios**:

   * *Una API para suscribirse a eventos del reproductor*: el Media SDK requiere que se invoquen varias API sencillas cuando se producen eventos en el reproductor.
   * *Una API que proporcione información del reproductor*: esta información incluye detalles como el nombre del contenido y la posición del cabezal de reproducción.

1. Añada la biblioteca [descargada](/help/sdk-implement/download-sdks.md#download-2x-sdks) al proyecto. Cree referencias locales a las clases para mayor comodidad.

   1. Expanda el `MediaSDK-js-v2.*.zip` archivo que descargó.
   1. Verify that the `MediaSDK.min.js` file exists in the `libs` directory:

   1. Host the `MediaSDK.min.js` file.

      Este archivo JavaScript principal debe alojarse en un servidor web al que se pueda acceder desde todas las páginas del sitio. Necesitará la ruta de estos archivos para el paso siguiente.

   1. Haga referencia a `MediaSDK.min.js` en todas las páginas del sitio.

      Include `MediaSDK` for JavaScript by adding the following line of code in the `<head>` or `<body>` tag on each page. Por ejemplo:

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Para comprobar rápidamente si la biblioteca de se ha importado correctamente, cree una instancia de la clase `ADB.va.MediaHeartbeatConfig`.

      >[!NOTE]
      >
      >From Version 2.1.0, the JavaScript SDK is compliant with the AMD and CommonJS module specifications, and `VideoHeartbeat.min.js` can also be used with compatible module loaders.

1. Para acceder fácilmente a las API, cree referencias locales a las clases `MediaHeartbeat`. 

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. Create a `MediaHeartbeatConfig` instance.

   Esta sección le ayudará a entender los parámetros de configuración de `MediaHeartbeat` y a seleccionar valores de configuración correctos en la instancia de `MediaHeartbeat` para conseguir un seguimiento preciso.

   Este es un ejemplo de una inicialización de `MediaHeartbeatConfig`:

   ```js
   //Media Heartbeat initialization 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = Configuration.HEARTBEAT.TRACKING_SERVER; 
   mediaConfig.playerName = Configuration.PLAYER.NAME; 
   mediaConfig.channel = Configuration.HEARTBEAT.CHANNEL; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = Configuration.HEARTBEAT.SDK; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = Configuration.HEARTBEAT.OVP; 
   ```

1. Implement the `MediaHeartbeatDelegate` protocol.

   ```js
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Replace <currentPlaybackTime> with the video player current playback time 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return <currentPlaybackTime>; 
   }; 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames> with the current playback QoS values.  
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(<bitrate>, <startuptime>, <fps>, <droppedFrames>); 
   };
   ```

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` and `MediaHeartbeatDelegate` to create the `MediaHeartbeat` instance.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the media session. Esta instancia se utilizará para todos los eventos de seguimiento posteriores.

   >[!TIP]
   >
   >`MediaHeartbeat` requiere una instancia de `AppMeasurement` para enviar llamadas a Adobe Analytics. Este es un ejemplo de una instancia de `AppMeasurement`:

   ```js
   var appMeasurement = new AppMeasurement(); 
   appMeasurement.visitor = visitor; 
   appMeasurement.trackingServer = "<visitor_namespace>.sc.omtrdc.net"; 
   appMeasurement.account = <rsid>; 
   appMeasurement.pageName = <page_name>; 
   appMeasurement.charSet = "UTF­8";
   ```

## Migración de la versión 1.x a 2.x en JavaScript

En la versión 2.x, todos los métodos públicos se incluyen en la clase `ADB.va.MediaHeartbeat` para facilitar el trabajo de los desarrolladores. Asimismo, todas las configuraciones están consolidadas en la clase `ADB.va.MediaHeartbeatConfig`. 

Para obtener información detallada sobre la migración de 1.x a 2.x, consulte [Migración de VHL 1.x a 2.x.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
