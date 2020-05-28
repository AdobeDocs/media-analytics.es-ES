---
title: Seguimiento de búsqueda con JavaScript 2.x
description: En este tema se describe la implementación del seguimiento de búsqueda mediante Media SDK en aplicaciones de navegador (JS).
uuid: 089947fb-8bae-4ae8-b215-53793620efd7
translation-type: tm+mt
source-git-commit: 5f274452b9ff5770908f7e2e450935be572a22ea
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 92%

---


# Seguimiento de búsqueda con JavaScript 2.x{#track-seeking-on-javascript}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

## Constantes de seguimiento de llamada a otro punto del contenido

| Nombre de la constante | Descripción     |
|---|---|
| `SeekStart` | Constante para el seguimiento del evento Iniciar llamada. |
| `SeekComplete` | Constante para rastrear el evento Finalización de llamada a otro punto del contenido. |

## Implemente la llamada a otro punto del contenido

1. Escuche los eventos de llamada a otro punto de la reproducción del reproductor de medios y, en la notificación del evento de inicio de la llamada a otro punto del contenido, rastree la búsqueda mediante el evento `SeekStart`:

   ```js
   _onSeekStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekStart);
   };
   ```

1. En la notificación de finalización de llamada a otro punto del contenido del reproductor, realice un seguimiento del final de la llamada a otro punto del contenido utilizando el evento `SeekComplete`.

   ```js
   _onSeekComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.SeekComplete);
   };
   ```

Consulte la situación de seguimiento [Reproducción de VOD con llamada a otro punto del contenido principal](/help/sdk-implement/tracking-scenarios/vod-seeking.md) para obtener más información.
