---
seo-title: Seguimiento del almacenamiento en búfer en Android
title: Seguimiento del almacenamiento en búfer en Android
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Seguimiento del almacenamiento en búfer en Android{#track-buffering-on-android}

>[!IMPORTANT]
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDks.](/help/sdk-implement/download-sdks.md)

## Constantes de seguimiento de búfer

| Nombre de la constante | Descripción     |
|---|---|
| `MediaHeartbeat.Event.BufferStart` | Constante para el seguimiento del evento de inicio de almacenamiento en búfer |
| `MediaHeartbeat.Event.BufferComplete` | Constante para el seguimiento del evento de finalización de almacenamiento en búfer |

## Implementar almacenamiento en búfer

1. Escuche los eventos de almacenamiento en búfer de reproducción procedentes del reproductor de medios y, cuando reciba la notificación del evento Inicio de almacenamiento en búfer, rastree el almacenamiento en búfer mediante el evento `BufferStart`:

   ```java
   public void onBufferStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferStart, null, null); 
   }
   ```

1. En la notificación de Finalización de almacenamiento en búfer procedente del reproductor de medios, rastree el final del almacenamiento en búfer con el evento `BufferComplete`:

   ```java
   public void onBufferComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete,null, null); 
   }
   ```

Consulte la situación de seguimiento [Reproducción de VOD con almacenamiento en búfer](/help/sdk-implement/tracking-scenarios/vod-buffering.md) para obtener más información.
