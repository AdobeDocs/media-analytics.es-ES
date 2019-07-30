---
seo-title: Seguimiento de llamada a otro punto del contenido en iOS
title: Seguimiento de llamada a otro punto del contenido en iOS
uuid: 1 d 31 ae 99-384 f -4 b 4 d-b 557-4018 db 177349
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Seguimiento de llamada a otro punto del contenido en iOS{#track-seeking-on-ios}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

## Constantes de seguimiento de llamada a otro punto del contenido

| Nombre de la constante | Descripción     |
|---|---|
| `ADBMediaHeartbeatEventSeekStart` | Constante para el seguimiento del evento Iniciar llamada. |
| `ADBMediaHeartbeatEventSeekComplete` | Constante para rastrear el evento Finalización de llamada a otro punto del contenido. |

## Implemente la llamada a otro punto del contenido

1. Escuche los eventos de llamada a otro punto de la reproducción del reproductor de medios y, en la notificación del evento de inicio de la llamada a otro punto del contenido, rastree la búsqueda mediante el evento `SeekStart`:

   ```
   - (void)onSeekStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekStart  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. En la notificación de finalización de llamada a otro punto del contenido del reproductor, realice un seguimiento del final de la llamada a otro punto del contenido utilizando el evento `SeekComplete`.

   ```
   - (void)onSeekComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventSeekComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

Consulte la situación de seguimiento [Reproducción de VOD con llamada a otro punto del contenido principal](/help/sdk-implement/tracking-scenarios/vod-seeking.md) para obtener más información.
