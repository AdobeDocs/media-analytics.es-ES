---
seo-title: Información general de configuración
title: Información general de configuración
uuid: 06 fefedb-b 0 c 8-4 f 7 d -90 c 8-e 374 cdde 1695
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Setup Overview{#setup-overview}

>[!IMPORTANT]
>
>Las siguientes instrucciones se aplican a los SDK de medios 2. x. Si va a implementar la versión 1.x del Media SDK, consulte la [documentación del Media SDK 1.x.](/help/sdk-implement/download-sdks.md) Para los integradores Primetime, consulte _la Documentación de Primetime Media SDK_ siguiente.


## Minimum Platform Version Support {#minimum-platform-version}

En la tabla siguiente se describen las versiones mínimas de plataforma compatibles con cada SDK, a partir del 19 de febrero de 2019.

| Sistema operativo o explorador | Se requiere la versión mínima |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0 + - Lollipop |
| Chrome | v 22 + |
| Mozilla | v 27 + |
| Safari | v 7 + |
| IE | v 11 + |

## Directrices generales de implementación {#section_965A3B699A8248DDB9B2B3EA3CC20E41}

En el seguimiento de medios, existen tres componentes de SDK principales:
* Configuración de Media Heartbeat: la configuración contiene la configuración básica de los informes.
* Delegado de Media Heartbeat: el delegado controla el tiempo de reproducción y el objeto QoS.
* Media Heartbeat: biblioteca principal que contiene miembros y métodos.

Complete los pasos de implementación siguientes:

1. Create a `MediaHeartbeatConfig` instance and set your config parameter values.

   |  Nombre de variable  | Descripción  | Requerido |  Valor predeterminado  |
   |---|---|:---:|---|
   | `trackingServer` | Servidor de seguimiento para el análisis de medios. Es distinto del servidor de seguimiento de Analytics. | Sí | Cadena vacía |
   | `channel` | Nombre del canal | No | Cadena vacía |
   | `ovp` | Nombre de la plataforma de medios en línea desde la que se distribuye el contenido. | No | Cadena vacía |
   | `appVersion` | Versión del SDK/aplicación del reproductor de medios | No | Cadena vacía |
   | `playerName` | Nombre del reproductor de medios en uso, por ejemplo, “AVPlayer”, “HTML5 Player”, “Mi reproductor personalizado”. | No | Cadena vacía |
   | `ssl` | Indica si las llamadas se deberían hacer mediante HTTPS. | No | false |
   | `debugLogging` | Indica si el registro de depuración está habilitado. | No | false |

1. Implement the `MediaHeartbeatDelegate`.

   |  Nombre del método  |  Descripción  | Requerido |
   | --- | --- | :---: |
   | `getQoSObject()` | Devuelve la instancia de `MediaObject` que contiene la información actual de QoS. Se llamará varias veces a este método durante una sesión de reproducción. La implementación del reproductor debe devolver siempre los datos de QoS más recientes que haya disponibles. | Sí |
   | `getCurrentPlaybackTime()` | Devuelve la posición actual del cabezal de reproducción. Para el seguimiento de vídeos VOD, el valor se especifica segundos después del comienzo del contenido multimedia. Para el seguimiento LINEAR/LIVE, el valor se especifica segundos después del principio del programa. | Sí |

   >[!TIP]
   >
   >El objeto Calidad del servicio (qos) es opcional. Si los datos de QoS están disponibles para su reproductor y desea realizar un seguimiento de dichos datos, es necesario el uso de las variables siguientes:

   | Nombre de variable | Descripción   | Requerido |
   | --- | --- | :---: |
   | `bitrate` | La velocidad de bits del contenido multimedia en bits por segundo. | Sí |
   | `startupTime` | Tiempo de inicio del contenido en milisegundos. | Sí |
   | `fps` | Fotogramas mostrados por segundo. | Sí |
   | `droppedFrames` | El número de fotogramas perdidos. | Sí |

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHertbeatConfig` and `MediaHertbeatDelegate` to create the `MediaHeartbeat` instance.

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and does not get deallocated until the end of the session. Esta instancia se utilizará para todos los eventos de seguimiento de medios posteriores.

   >[!TIP]
   >
   >`MediaHeartbeat` requiere una instancia de `AppMeasurement` enviar llamadas a Adobe Analytics.

1. Combine todos los fragmentos.

   El siguiente código de ejemplo utiliza nuestro SDK de JavaScript 2.x para un reproductor de vídeo HTML5:

   ```javascript
   // Create local references to the heartbeat classes 
   var MediaHeartbeat = ADB.va.MediaHeartbeat; 
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig; 
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate; 
   
   //Media Heartbeat Config 
   var mediaConfig = new MediaHeartbeatConfig(); 
   mediaConfig.trackingServer = "namespace.hb.omtrdc.net"; 
   mediaConfig.playerName = "HTML5 Basic"; 
   mediaConfig.channel = "Video Channel"; 
   mediaConfig.debugLogging = true; 
   mediaConfig.appVersion = "2.0"; 
   mediaConfig.ssl = false; 
   mediaConfig.ovp = ""; 
   
   // Media Heartbeat Delegate 
   var mediaDelegate = new MediaHeartbeatDelegate(); 
   
   // Set mediaDelegate CurrentPlaybackTime 
   mediaDelegate.getCurrentPlaybackTime = function() { 
       return video.currentTime; 
   }; 
   
   // Set mediaDelegate QoSObject - OPTIONAL 
   mediaDelegate.getQoSObject = function() { 
       return MediaHeartbeat.createQoSObject(video.bitrate,  
                                             video.startuptime,  
                                             video.fps,  
                                             video.droppedframes); 
   } 
   // Create mediaHeartbeat instance      
   this.mediaHeartbeat =  
     new MediaHeartbeat(mediaDelegate, mediaConfig, appMeasurementInstance);  
   ```

## Validación {#section_D4D46F537A4E442B8AB0BB979DDAA4CC}

Las implementaciones de medios constan de dos tipos de llamadas de seguimiento:

* Las llamadas de inicio de medios y publicidad se envían directamente al servidor de AppMeasurement.
* Las llamadas de Heartbeat se envían al servidor de seguimiento de Heartbeat al inicio, cada diez segundos para el contenido y cada segundo para la publicidad.

El seguimiento de medios funciona del mismo modo en todas las plataformas, equipos de escritorio y dispositivos móviles. Actualmente, el seguimiento de audio funciona en plataformas móviles. En todas las llamadas de seguimiento hay algunas variables universales clave que se deben validar:

* **Appmeasurement (Analytics)**
Para obtener más información sobre las opciones de servidor, consulte [Rellenar correctamente la variable trackingserver y trackingserversecure.](https://marketing.adobe.com/resources/help/kb/en_US/analytics/kb/determining-data-center.html)

   >[!IMPORTANT]
   >
   >Se requiere un servidor de seguimiento RDC o una resolución CNAME para un servidor RDC para el servicio de ID de visitante de Experience Cloud.

   The analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

* **Latidos (Análisis de medios)**
Siempre tiene el formato "`[namespace].hb.omtrdc.net`, donde"`[namespace]`define su empresa de inicio de sesión y lo proporciona Adobe.

## SDK 1.x Documentation {#section_acj_tkk_t2b}

| SDK de Video Analytics 1. x  | Guías para desarrolladores (solo PDF) |
| --- | --- |
| Android | [Configurar para Android ](vhl-dev-guide-v15_android.pdf) |
| Apple TV | [Configurar para Apple TV ](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Configurar para Chromecast ](chromecast_1.x_sdk.pdf) |
| iOS | [Configurar para iOS ](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [Configurar para JavaScript ](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/android/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> DHLS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/dhls/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS:   [Configure Media Analytics](https://help.adobe.com/en_US/primetime/psdk/ios/1.4/index.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [Configurar para TVML ](vhl_tvml.pdf) |

## Documentación del Media SDK de Primetime {#primetime-docs}

* [Guías del usuario Primetime](https://helpx.adobe.com/primetime/user-guide.html)
