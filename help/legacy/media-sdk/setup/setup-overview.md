---
title: Explicación de la implementación de Media SDK
description: Obtenga información sobre cómo configurar Media SDK para el seguimiento de contenido en las aplicaciones móviles, OTT y de navegador (JS).
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: 0083869ae4248134dea18a87b9d4ce563eeed1a4
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 94%

---

# Heredado - Información general de la configuración de Media SDK {#setup-overview}

Después de descargar el Media SDK para su aplicación de vídeo o reproductor, siga la información de esta sección para configurar e implementar el Media SDK.


## Directrices generales de implementación {#general-implementation-guidelines}

Hay tres componentes principales de SDK utilizados en el seguimiento con servicios de medios de streaming:
* Media Heartbeat Config-El `MediaHeartbeatConfig` contiene la configuración básica para la creación de informes.
* Media Heartbeat Delegate-El `MediaHeartbeatDelegate` controla el tiempo de reproducción y el objeto QoS.
* Media Heartbeat-La `MediaHeartbeat` es la biblioteca principal que contiene miembros y métodos.

## Implementación del SDK de medios de streaming

Para configurar y utilizar el SDK de medios de streaming, complete los siguientes pasos de implementación:

1. Cree una instancia `MediaHeartbeatConfig` y establezca los valores de sus parámetros de configuración.

   |  Nombre de variable  | Descripción  | Requerido |  Valor predeterminado  |
   |---|---|:---:|---|
   | `trackingServer` | Servidor de seguimiento para análisis de medios. Esto es diferente al servidor de seguimiento de Analytics. | Sí | Cadena vacía |
   | `channel` | Nombre del canal | No | Cadena vacía |
   | `ovp` | Nombre de la plataforma de medios en línea desde la que se distribuye el contenido. | No | Cadena vacía |
   | `appVersion` | La versión del SDK/aplicación del reproductor de medios | No | Cadena vacía |
   | `playerName` | Nombre del reproductor de medios en uso como &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;Mi reproductor personalizado&quot; | No | Cadena vacía |
   | `ssl` | Indica si las llamadas deben realizarse a través de HTTPS | No | false |
   | `debugLogging` | Indica si el registro de depuración está habilitado | No | false |

1. Implementación de `MediaHeartbeatDelegate`.

   |  Nombre del método  |  Descripción  | Requerido |
   | --- | --- | :---: |
   | `getQoSObject()` | Devuelve la instancia de `MediaObject` que contiene la información actual de QoS. Se llamará varias veces a este método durante una sesión de reproducción. La implementación del reproductor debe devolver siempre los datos de QoS más recientes que haya disponibles. | Sí |
   | `getCurrentPlaybackTime()` | Devuelve la posición actual del cabezal de reproducción. <br /> Para el seguimiento de vídeos VOD, el valor se especifica segundos después del comienzo del elemento de medios. <br /> Para el streaming en directo, si el reproductor no proporciona información acerca de la duración del contenido, el valor se puede especificar como el número de segundos desde la medianoche (UTC) de ese día. <br /> Nota: Cuando se utilizan marcadores de progreso, la duración del contenido es obligatoria y el cabezal de reproducción debe actualizarse como número de segundos desde el principio del elemento de medios, empezando por 0. | Sí |

   >[!TIP]
   >
   >El objeto de calidad de servicio (QoS) es opcional. Si los datos de QoS están disponibles para el reproductor y desea rastrearlos, se requieren las siguientes variables:

   | Nombre de variable | Descripción   | Requerido |
   | --- | --- | :---: |
   | `bitrate` | Velocidad de bits del medio en bits por segundo. | Sí |
   | `startupTime` | Tiempo de activación del inicio del medio en milisegundos. | Sí |
   | `fps` | Los fotogramas mostrados por segundo. | Sí |
   | `droppedFrames` | Número de fotogramas perdidos hasta ahora. | Sí |

1. Cree la instancia de `MediaHeartbeat`.

   Utilice `MediaHertbeatConfig` y `MediaHertbeatDelegate` para crear la instancia `MediaHeartbeat`.

   >[!IMPORTANT]
   >
   >Asegúrese de que la instancia de `MediaHeartbeat` es accesible y no se desasigna hasta el final de la sesión. Esta instancia se utilizará para todos los eventos de seguimiento de medios posteriores.

   >[!TIP]
   >
   >`MediaHeartbeat` requiere una instancia de `AppMeasurement` para enviar llamadas a Adobe Analytics.

1. Combine todas las piezas.

   El siguiente código de ejemplo utiliza nuestro SDK JavaScript 2.x para un reproductor de vídeo HTML5:

   ```javascript
   // Create local references to the heartbeat classes
   var MediaHeartbeat = ADB.va.MediaHeartbeat;
   var MediaHeartbeatConfig = ADB.va.MediaHeartbeatConfig;
   var MediaHeartbeatDelegate = ADB.va.MediaHeartbeatDelegate;
   
   //Media Heartbeat Config
   var mediaConfig = new MediaHeartbeatConfig();
   mediaConfig.trackingServer = "[your_namespace].hb.omtrdc.net";
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

## Validación  {#validate}

Las implementaciones de seguimiento de Media Analytics generan dos tipos de llamadas de seguimiento:

* Las llamadas de inicio de contenido y anuncio se envían directamente al servidor de Adobe Analytics (AppMeasurement).
* Las llamadas de Heartbeat se envían al servidor de seguimiento de Media Analytics (latidos), se procesan y se pasan al servidor de Adobe Analytics.

* **Servidor de Adobe Analytics (AppMeasurement)** Para obtener más información sobre las opciones del servidor de seguimiento, consulte [Rellenar correctamente las variables trackingServer y trackingServerSecure.](https://helpx.adobe.com/es/analytics/kb/determining-data-center.html)

  >[!IMPORTANT]
  >
  >Es necesario un servidor de seguimiento RDC o CNAME que se resuelva en un servidor RDC para el servicio ID de visitante de Experience Cloud.

  El servidor de seguimiento de análisis debe finalizar en “`.sc.omtrdc.net`” o ser CNAME.

* ** Servidor de Media Analytics (latidos)**
Siempre tiene el formato “`[your_namespace].hb.omtrdc.net`”. El valor de “`[your_namespace]`” especifica su empresa y lo proporciona Adobe.

El seguimiento de medios funciona del mismo modo en todas las plataformas, equipos de escritorio y dispositivos móviles. Actualmente, el seguimiento de audio funciona en plataformas móviles. En todas las llamadas de seguimiento hay algunas variables universales clave que se deben validar:
