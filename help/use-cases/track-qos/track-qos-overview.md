---
title: Seguimiento de la calidad de la experiencia explicada
description: Información general sobre el seguimiento de la calidad de la experiencia (QoE, QoS) mediante Media SDK.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
exl-id: af5f3372-a9a5-46ea-9c2f-81b0f5c96ccf
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 98%

---

# Información general{#overview}

En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x.

>[!IMPORTANT]
>
>Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

El seguimiento de la calidad de la experiencia incluye la calidad del servicio (QoS) y el seguimiento de errores. Ambos son elementos opcionales y **no** son necesarios para las implementaciones principales de contenido. Puede utilizar la API del reproductor de contenido para identificar las variables relacionadas con la calidad de servicio y el seguimiento de errores. Estos son los elementos clave del seguimiento de la calidad de la experiencia:

## Eventos del reproductor {#player-events}

### En cualquier cambio de métrica de QoS:

Cree o actualice la instancia del objeto QoS para la reproducción. [Referencia de API de QoS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### En todos los eventos de cambio de velocidad de bits

La llamada `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implementación de QOS

1. Identifique cuándo cambia alguna de las métricas de QoS durante la reproducción de contenido, cree el objeto `MediaObject` mediante el uso de la información de QoS y actualice la nueva información de QoS.

   Variables QoSObject:

   >[!TIP]
   >
   >Estas variables solo son necesarias si planea realizar seguimientos de QoS.

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
   >Actualice el objeto QoS e invoque el evento de cambio de velocidad de bits en cada cambio. Esto proporciona los datos de QoS más precisos.

El siguiente código de ejemplo utiliza el SDK JavaScript 2.x para un reproductor de contenidos HTML5. Este código debe utilizarse con el código de reproducción de contenidos principal.

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
