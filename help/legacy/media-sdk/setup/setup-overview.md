---
title: Explicación de la implementación de Media SDK
description: Obtenga información sobre cómo configurar Media SDK para el seguimiento de contenido en las aplicaciones móviles, OTT y de navegador (JS).
uuid: 06fefedb-b0c8-4f7d-90c8-e374cdde1695
exl-id: a175332e-0bdc-44aa-82cb-b3f879e7abfc
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/DsVDPsePWd123v5D8OdC2zUn52IWAOwh6QxcpvB1FIs
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c8add8f2-4250-4fd9-9cde-9707036c567did: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 626
ht-degree: 81%

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
   | `getCurrentPlaybackTime()` | Devuelve la posición actual del cabezal de reproducción. <br /> Para el seguimiento de VOD, el valor se especifica segundos después del comienzo del elemento de medios. <br /> Para el streaming en directo, si el reproductor no proporciona información acerca de la duración del contenido, el valor se puede especificar como el número de segundos desde la medianoche (UTC) de ese día. <br /> Nota: Cuando se utilizan marcadores de progreso, la duración del contenido es obligatoria y el cabezal de reproducción debe actualizarse como número de segundos desde el principio del elemento de medios, empezando por 0. | Sí |

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

## Validación {#validate}

Las implementaciones de seguimiento de Media Analytics generan dos tipos de llamadas de seguimiento:

* Las llamadas de inicio de contenido y anuncio se envían directamente al servidor de Adobe Analytics (AppMeasurement).
* Las llamadas de Heartbeat se envían al servidor de seguimiento de Media Analytics (latidos), se procesan y se pasan al servidor de Adobe Analytics.

* **Servidor de Adobe Analytics (AppMeasurement)**
Para obtener más información acerca de las opciones del servidor de seguimiento, vea [Rellenar correctamente las variables trackingServer y trackingServerSecure.](https://helpx.adobe.com/es/analytics/kb/determining-data-center.html)

  >[!IMPORTANT]
  >
  >Es necesario un servidor de seguimiento RDC o CNAME que se resuelva en un servidor RDC para el servicio ID de visitante de Experience Cloud.

  El servidor de seguimiento de análisis debe finalizar en “`.sc.omtrdc.net`” o ser CNAME.

* Servidor de ** Media Analytics (latidos)**
Siempre tiene el formato &quot;`[your_namespace].hb.omtrdc.net`&quot;. El valor de “`[your_namespace]`” especifica su empresa y lo proporciona Adobe.

El seguimiento de medios funciona del mismo modo en todas las plataformas, equipos de escritorio y dispositivos móviles. Actualmente, el seguimiento de audio funciona en plataformas móviles. En todas las llamadas de seguimiento hay algunas variables universales clave que se deben validar:
