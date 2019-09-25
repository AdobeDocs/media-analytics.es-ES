---
seo-title: Seguimiento de la calidad de la experiencia en iOS
title: Seguimiento de la calidad de la experiencia en iOS
uuid: cae2c142-ed39-4234-a711-765dcabc5415
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Seguimiento de la calidad de la experiencia en iOS{#track-quality-of-experience-on-ios}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

## Implementación de QOS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   Variables QoSObject:

   | Variable | Descripción | Requerido |
   | --- | --- | :---: |
   | `bitrate` | Velocidad de bits actual | Sí |
   | `startupTime` | Hora de inicio | Sí |
   | `fps` | Valor FPS | Sí |
   | `droppedFrames` | Número de fotogramas perdidos | Sí |

   >[!TIP]
   >
   >Estas variables solo son necesarias si planea realizar un seguimiento de QoS.

   Creación del objeto de QoS:

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE] 
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. Asegúrese de que el método `getQoSObject` devuelve la información de QoS más actual.
1. Cuando la velocidad de bits de la reproducción cambie, invoque el evento `BitrateChange` en la instancia de Media Heartbeat:

   ```
   - (void)onBitrateChange:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

   >[!IMPORTANT]
   >
   >Actualice el objeto QoS y llame al evento de cambio de velocidad de bits en cada cambio de velocidad de bits. Esto proporciona los datos de QoS más precisos.

