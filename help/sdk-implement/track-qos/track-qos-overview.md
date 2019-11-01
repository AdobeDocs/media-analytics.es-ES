---
title: Información general
description: Información general sobre la calidad de seguimiento de la experiencia (QoE, QoS) mediante el SDK de medios.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Información general{#overview}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Puede utilizar la API del reproductor de medios para identificar las variables relacionadas con QoS y el seguimiento de errores. Estos son los elementos clave del seguimiento de la calidad de la experiencia:

## Eventos del reproductor {#player-events}

### En cualquier cambio de métrica de QoS:

Cree o actualice la instancia del objeto QoS para la reproducción. [Referencia de API de QoS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### En todos los eventos de cambio de velocidad de bits

La llamada `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implementación de QOS

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

   Variables QoSObject:

   >[!TIP]
   >
   >Estas variables solo son necesarias si planea realizar un seguimiento de QoS.

   | Variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `bitrate` | Velocidad de bits actual | Sí |
   | `startupTime` | Hora de inicio | Sí |
   | `fps` | Valor FPS | Sí |
   | `droppedFrames` | Número de fotogramas perdidos | Sí |

1. Asegúrese de que el método `getQoSObject()` devuelve la información de QoS más actual.
1. Cuando la velocidad de bits de la reproducción cambie, invoque el evento `BitrateChange` en la instancia de Media Heartbeat.

   >[!IMPORTANT]
   >
   >Actualice el objeto QoS y llame al evento de cambio de velocidad de bits en cada cambio de velocidad de bits. Esto proporciona los datos de QoS más precisos.

El siguiente código de muestra utiliza el SDK de JavaScript 2.x para un reproductor de medios HTML5. Debe utilizar este código con el código de reproducción de medios principal.

```js
var mediaDelegate = new MediaHeartbeatDelegate(); 
...  
 
// This is called periodically by MediaHeartbeat instance 
mediaDelegate.prototype.getQoSObject = function() { 
    return this.qosInfo; 
}; 
 
if (e.type == "qos_update") { 
    var qosInfo = MediaHeartbeat.createQoSObject(<BITRATE>,<STARTUP_TIME>,<FPS>,<DROPPED_FRAMES>); 
    mediaDelegate.qosInfo = qosInfo; 
}; 
 
if (e.type == "bitrate_change") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
};
```

