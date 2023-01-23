---
title: Aprenda a controlar el almacenamiento en búfer con JavaScript 3.x
description: Aprenda a rastrear eventos de almacenamiento en búfer en aplicaciones de explorador (JS).
exl-id: c6941942-02f9-4f9c-99ad-0c52ed2f793b
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '120'
ht-degree: 100%

---

# Seguimiento del almacenamiento en búfer con JavaScript 3.x{#track-buffering-on-javascript}

En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 3.x.

>[!IMPORTANT]
>
>Si va a implementar cualquier versión anterior del SDK, puede descargar las guías del desarrollador aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

## Constantes de seguimiento de búfer

| Nombre de la constante | Descripción     |
|---|---|
| `BufferStart` | Constante para el seguimiento del evento de inicio de almacenamiento en búfer |
| `BufferComplete` | Constante para el seguimiento del evento de finalización de almacenamiento en búfer |

## Implementar almacenamiento en búfer

1. Escuche los eventos de almacenamiento en búfer de reproducción procedentes del reproductor de medios y, cuando reciba la notificación del evento Inicio de almacenamiento en búfer, rastree el almacenamiento en búfer mediante el evento `BufferStart`.

   ```js
   _onBufferStart = function() {
       tracker.trackEvent(ADB.Media.Event.BufferStart);
   };
   ```

1. En la notificación de Finalización de almacenamiento en búfer procedente del reproductor de medios, rastree el final del almacenamiento en búfer con el evento `BufferComplete`.

   ```js
   _onBufferComplete = function() {
       tracker.trackEvent(ADB.Media.Event.BufferComplete);
   };
   ```

Consulte la situación de seguimiento [Reproducción de VOD con almacenamiento en búfer](/help/use-cases/tracking-scenarios/vod-buffering.md) para obtener más información.
