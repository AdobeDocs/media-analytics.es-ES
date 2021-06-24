---
title: Obtenga información sobre cómo rastrear el almacenamiento en búfer en Android
description: Obtenga información sobre cómo rastrear eventos de almacenamiento en búfer en Android.
uuid: f16ce76d-1db3-4b51-8c98-54cb781f71d7
exl-id: fcea2ef8-53c5-41fb-8b70-06599c2d9cbf
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 87%

---

# Seguimiento del almacenamiento en búfer en Android{#track-buffering-on-android}

>[!IMPORTANT]
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

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
