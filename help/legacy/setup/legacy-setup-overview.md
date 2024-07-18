---
title: Explicación de la implementación de los SDK para medios heredados
description: Aprenda a configurar el SDK de medios **legacy** 2.x para el seguimiento de medios en sus aplicaciones móviles, OTT y de navegador (JS).
feature: Media Analytics
role: User, Admin, Data Engineer
exl-id: d94ede3e-95f8-4591-9833-ef39aff12ba9
source-git-commit: a7d897c6f6fbc6ed0d5b71f5801ab18ee21f0411
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 99%

---

# Información general de la configuración del SDK de medios de streaming heredado 2.x{#setup-overview}

Las instrucciones de esta sección se aplican a la variable Media SDK 2.x. **heredado**.

* Para obtener información sobre la implementación de una versión 1.x del Media SDK, consulte la [Documentación del Media SDK 1.x.](/help/getting-started/download-sdks.md)

* Para los integradores de Primetime, consulta la _Documentación del SDK de Primetime Media_.

>[!IMPORTANT]
>
>Con la finalización de la compatibilidad con los SDK para móviles de la versión 4 el 31 de agosto de 2021, Adobe también dejará de ofrecer compatibilidad con los SDK de Media Analytics para iOS y Android.  Para obtener más información, consulte [Preguntas frecuentes sobre el fin de la asistencia del SDK de Media Analytics](/help/additional-resources/end-of-support-faqs.md).


## Compatibilidad con versiones con la plataforma mínima requerida {#minimum-platform-version}

En la tabla siguiente se describen las versiones de plataforma mínimas admitidas para cada SDK a partir del 19 de febrero de 2019.

| OS/Browser | Versión mínima requerida |
| --- | --- |
| iOS | iOS 6+ |
| Android | Android 5.0+ - Lollipop |
| Chrome | v22+ |
| Mozilla | v27+ |
| Safari | v7+ |
| IE | v11+ |

## Directrices generales de implementación {#general-implementation-guidelines}

Hay tres componentes principales del SDK involucrados en el seguimiento de medios:
* Configuración de Media Heartbeat: La configuración contiene la configuración básica para la creación de informes.
* Delegado de Media Heartbeat: El delegado controla el tiempo de reproducción y el objeto QoS.
* Media Heartbeat: La biblioteca principal que contiene miembros y métodos.

Complete los pasos siguientes de la implementación:

1. Cree una instancia de `MediaHeartbeatConfig` y establezca los valores de configuración de parámetros.

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

## Documentación de SDK 1.x {#sdk-1x-documentation}

| SDK de Video Analytics 1.x  |  Guías para desarrolladores (solo PDF) |
| --- | --- |
| Android | [Configurar para Android](vhl-dev-guide-v15_android.pdf) |
| Apple TV | [Configurar para Apple TV](vhl-dev-guide-v1x_appletv.pdf) |
| Chromecast | [Configurar para Chromecast](chromecast_1.x_sdk.pdf) |
| iOS | [Configurar para iOS](vhl-dev-guide-v15_ios.pdf) |
| JavaScript | [Configurar para JavaScript](vhl-dev-guide-v15_js.pdf) |
| Primetime | <ul> <li> Android: [Configurar Media Analytics](https://helpx.adobe.com/es/support/primetime.html) </li> <li> DHLS: [Configurar Media Analytics](https://helpx.adobe.com/es/support/primetime.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> <li> iOS: [Configurar Media Analytics](https://helpx.adobe.com/es/support/primetime.html#PSDKs-task-Initialize_and_configure_video_analytics_) </li> </ul> |
| TVML | [Configurar para TVML](vhl_tvml.pdf) |

## Documentación de Media SDK de Primetime {#primetime-docs}

* [Guías del usuario de Primetime](https://helpx.adobe.com/es/support/primetime.html)
