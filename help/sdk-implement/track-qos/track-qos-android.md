---
title: Seguimiento de la calidad de la experiencia en Android
description: En este tema se describe la implementación del seguimiento de calidad de experiencia (QoE, QoS) mediante el SDK de medios en Android.
uuid: 81ff3939-48a6-45c1-8837-dfa33490559
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Seguimiento de la calidad de la experiencia en Android{#track-quality-of-experience-on-android}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

## QoS de implementación

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

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

   Creación del objeto de QoS:

   ```java
   MediaObject qosObject =  
     MediaHeartbeat.createQoSObject(<BITRATE>,  
                                    <STARTUP_TIME>,  
                                    <FPS>,  
                                    <DROPPED_FRAMES>);
   ```

1. Asegúrese de que el método `getQoSObject()` devuelve la información de QoS más actual.
1. Cuando la velocidad de bits de la reproducción cambie, invoque el evento `BitrateChange` en la instancia de Media Heartbeat:

   ```java
   public void onBitrateChange(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null); 
   } 
   ```

   >[!IMPORTANT]
   >
   >Actualice el objeto QoS y llame al evento de cambio de velocidad de bits en cada cambio de velocidad de bits. Esto proporciona los datos de QoS más precisos.

