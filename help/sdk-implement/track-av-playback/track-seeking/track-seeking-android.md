---
seo-title: Seguimiento de llamada a otro punto del contenido en Android
title: Seguimiento de llamada a otro punto del contenido en Android
uuid: 65 addd 99-eebf -4 a 80-8 b 4 a-d 5 fbdff 8 ab 06
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

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
