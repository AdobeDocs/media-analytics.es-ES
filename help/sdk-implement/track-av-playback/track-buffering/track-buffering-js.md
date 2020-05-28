---
title: Seguimiento del almacenamiento en búfer mediante JavaScript 2.x
description: Describe el seguimiento de eventos de almacenamiento en búfer en aplicaciones de navegador (JS).
uuid: c380cf2c-7729-4d4a-a4da-581bd94a5896
translation-type: tm+mt
source-git-commit: 8235fee973623c168dbf83f43aa85f13b4e06cff
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 91%

---


# Seguimiento del almacenamiento en búfer mediante JavaScript 2.x{#track-buffering-on-javascript}

>[!IMPORTANT]
>
>En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x. Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/sdk-implement/download-sdks.md)

## Constantes de seguimiento de búfer

| Nombre de la constante | Descripción     |
|---|---|
| `BufferStart` | Constante para el seguimiento del evento de inicio de almacenamiento en búfer |
| `BufferComplete` | Constante para el seguimiento del evento de finalización de almacenamiento en búfer |

## Implementar almacenamiento en búfer

1. Escuche los eventos de almacenamiento en búfer de reproducción procedentes del reproductor de medios y, cuando reciba la notificación del evento Inicio de almacenamiento en búfer, rastree el almacenamiento en búfer mediante el evento `BufferStart`.

   ```js
   _onBufferStart = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferStart);
   };
   ```

1. En la notificación de Finalización de almacenamiento en búfer procedente del reproductor de medios, rastree el final del almacenamiento en búfer con el evento `BufferComplete`.

   ```js
   _onBufferComplete = function() {
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BufferComplete);
   };
   ```

Consulte la situación de seguimiento [Reproducción de VOD con almacenamiento en búfer](/help/sdk-implement/tracking-scenarios/vod-buffering.md) para obtener más información.
