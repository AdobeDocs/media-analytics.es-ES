---
title: Seguimiento de llamada a otro punto del contenido en Android
description: En este tema se describe la implementación del seguimiento de búsqueda mediante el SDK de medios en Android.
uuid: 65addd99-eebf-4a80-8b4a-d5fbdff8ab06
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Seguimiento de llamada a otro punto del contenido en Android{#track-seeking-on-android}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

## Constantes de seguimiento de llamada a otro punto del contenido

| Nombre de la constante | Descripción     |
|---|---|
| `MediaHeartbeat.Event.SeekStart` | Constante para el seguimiento del evento Iniciar llamada. |
| `MediaHeartbeat.Event.SeekComplete` | Constante para rastrear el evento Finalización de llamada a otro punto del contenido. |

## Implemente la llamada a otro punto del contenido

1. Escuche los eventos de llamada a otro punto de la reproducción del reproductor de medios y, en la notificación del evento de inicio de la llamada a otro punto del contenido, rastree la búsqueda mediante el evento `SeekStart`:

   ```java
   public void onSeekStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekStart, null, null); 
   }
   ```

1. En la notificación de finalización de llamada a otro punto del contenido del reproductor, realice un seguimiento del final de la llamada a otro punto del contenido utilizando el evento `SeekComplete`.

   ```java
   public void onSeekComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete, null, null); 
   }
   ```

Consulte la situación de seguimiento [Reproducción de VOD con llamada a otro punto del contenido principal](/help/sdk-implement/tracking-scenarios/vod-seeking.md) para obtener más información.
