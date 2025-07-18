---
title: Descubra cómo rastrear la calidad de la experiencia en Android
description: Obtenga información acerca de la implementación del seguimiento de calidad de experiencia (QoE, QoS) mediante Media SDK en Android.
uuid: 81ff3939-48a6-45c1-8837-ddfa33490559
exl-id: cee8b119-bca2-4a5c-8111-2b49f7eede66
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 89%

---

# Seguimiento de la calidad de la experiencia en Android{#track-quality-of-experience-on-android}

En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x.

>[!IMPORTANT]
>
>Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

## Implementación de QoS

1. Identifique cuándo cambia la velocidad de bits durante la reproducción de contenido y cree la instancia de `MediaObject` con la información de QoS.

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
   >Actualice el objeto QoS e invoque el evento de cambio de velocidad de bits en cada cambio. Esto proporciona los datos de QoS más precisos.
