---
seo-title: Información general
title: Información general
uuid: 4 d 73 c 47 f-d 0 a 4-4228-9040-d 6432311 c 9 eb
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Información general{#overview}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Puede utilizar la API de reproductor de medios para identificar las variables relacionadas con qos y el seguimiento de errores. Estos son los elementos clave del seguimiento de la calidad de la experiencia:

## Eventos del reproductor {#player-events}

### En cualquier cambio de métrica de QoS:

Cree o actualice la instancia del objeto QoS para la reproducción. [Referencia de la API de qos](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### En todos los eventos de cambio de velocidad de bits

La llamada `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implemement QOS

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

   Variables QoSObject:

   >[!TIP]
   >
   >Estas variables solo se requieren si planea rastrear qos.

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
   >Actualice el objeto qos y llame al suceso change de velocidad de bits en cada cambio de velocidad de bits. Esto proporciona los datos de QoS más precisos.

El siguiente código de ejemplo utiliza el SDK 2. x de JavaScript para un reproductor de medios HTML 5. Debe utilizar este código con el código de reproducción multimedia principal.

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

