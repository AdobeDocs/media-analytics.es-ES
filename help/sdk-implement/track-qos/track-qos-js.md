---
seo-title: Seguimiento de la calidad de la experiencia en JavaScript
title: Seguimiento de la calidad de la experiencia en JavaScript
uuid: 3 bc 762 a 2-9706-4 b 62-aa 91-747 f 461 dd 13 d
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Seguimiento de la calidad de la experiencia en JavaScript{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](../../sdk-implement/download-sdks.md)

## Implemement QOS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

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

   Creación del objeto de QoS:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>); 
   ```

1. Cuando la velocidad de bits de la reproducción cambie, invoque el evento `BitrateChange` en la instancia de Media Heartbeat:

   ```js
   _onBitrateChange = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
   };
   ```

   >[!IMPORTANT]
   >
   >Actualice el objeto qos y llame al suceso change de velocidad de bits en cada cambio de velocidad de bits. Esto proporciona los datos de QoS más precisos.

1. Asegúrese de que el método `getQoSObject()` devuelve la información de QoS más actual.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Consulte [Información general](../../sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >El seguimiento de los errores del reproductor de medios no detendrá la sesión de seguimiento de medios. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

