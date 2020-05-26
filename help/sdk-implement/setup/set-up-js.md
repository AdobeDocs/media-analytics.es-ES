---
title: Configuración de JavaScript
description: Configuración de la aplicación de Media SDK para la implementación en JavaScript.
uuid: 0269d8ad-0af8-4bf1-9d15-e06c2952a005
translation-type: ht
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a
workflow-type: ht
source-wordcount: '393'
ht-degree: 100%

---


# Configuración de JavaScript {#set-up-javascript}

## Requisitos previos

* **Obtenga parámetros de configuración válidos**: Estos parámetros se pueden obtener de un representante de Adobe una vez creada la cuenta de Analytics.
* **Implemente`AppMeasurement`para JavaScript en la aplicación de contenido**: Para obtener más información sobre la documentación del SDK de Adobe Mobile, consulte [Implementación de Analytics utilizando JavaScript.](https://docs.adobe.com/content/help/es-ES/analytics/implementation/js/overview.html)

* **Proporcione las siguientes capacidades en su reproductor de contenidos**:

   * *Una API para suscribirse a eventos del reproductor*: Media SDK requiere que llame a un conjunto de API simples cuando se produzcan eventos en el reproductor.
   * *Una API que proporciona información del reproductor*: Esta información incluye detalles como el nombre del medio y la posición del cabezal de reproducción.

1. Añada la biblioteca [descargada](/help/sdk-implement/download-sdks.md#download-2x-sdks) al proyecto. Cree referencias locales a las clases para mayor comodidad.

   1. Expanda el archivo `MediaSDK-js-v2.*.zip` que descargó.
   1. Compruebe si el archivo `MediaSDK.min.js` existe en el directorio `libs`:

   1. Aloje el archivo `MediaSDK.min.js`.

      Este archivo JavaScript principal debe alojarse en un servidor web al que se pueda acceder desde todas las páginas del sitio. Necesita la ruta a estos archivos para el siguiente paso.

   1. Haga referencia a `MediaSDK.min.js` en todas las páginas del sitio.

      Incluya `MediaSDK` para JavaScript agregando la línea de código siguiente en la etiqueta `<head>` o `<body>` de cada página. Por ejemplo:

      ```
      <script type="text/javascript" 
      src="https://INSERT-DOMAIN-AND-PATH-TO-CODE-HERE/MediaSDK.min.js"></script>
      ```

   1. Para comprobar rápidamente si la biblioteca de se ha importado correctamente, cree una instancia de la clase `ADB.va.MediaHeartbeatConfig`.

      >[!NOTE]
      >
      >Desde la versión 2.1.0, el SDK de JavaScript es compatible con las especificaciones del módulo AMD y CommonJS, y `VideoHeartbeat.min.js` también se puede utilizar con módulos de carga compatibles.

1. Para acceder fácilmente a las API, cree referencias locales a las clases `MediaHeartbeat`.

   ```js
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   ```

1. Cree una instancia de `MediaHeartbeatConfig`.

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

1. Implemente el protocolo de `MediaHeartbeatDelegate`.

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

1. Cree la instancia de `MediaHeartbeat`.

   Utilice `MediaHeartbeatConfig` y `MediaHeartbeatDelegate` para crear la instancia `MediaHeartbeat`.

   ```js
   this.mediaHeartbeat = new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurement);
   ```

   >[!IMPORTANT]
   >
   >Asegúrese de que la instancia de `MediaHeartbeat` es accesible y no se desasigna hasta el final de la sesión de contenido. Esta instancia se utilizará para todos los eventos de seguimiento posteriores.

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
