---
title: Obtenga información sobre cómo rastrear el almacenamiento en búfer en Roku
description: Obtenga información sobre cómo rastrear eventos de almacenamiento en búfer en Roku.
uuid: 6666b270-9aa3-42ff-95a8-f12502022d47
exl-id: 73b10b42-02ab-47f8-8250-58f03c5e0dd1
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 100%

---

# Seguimiento del almacenamiento en búfer en Roku{#track-buffering-on-roku}

En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x.

>[!IMPORTANT]
>
>Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

## Constantes de seguimiento de búfer

| Nombre de la constante | Descripción     |
|---|---|
| `BufferStart` | Constante para el seguimiento del evento de inicio de almacenamiento en búfer |
| `BufferComplete` | Constante para el seguimiento del evento de finalización de almacenamiento en búfer |

## Implementar almacenamiento en búfer

1. Escuche los eventos de almacenamiento en búfer de reproducción procedentes del reproductor de medios y, cuando reciba la notificación del evento Inicio de almacenamiento en búfer, rastree el almacenamiento en búfer mediante el evento `BufferStart`.

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_START, bufferInfo, bufferContextData)
   ```

1. En la notificación de Finalización de almacenamiento en búfer procedente del reproductor de medios, rastree el final del almacenamiento en búfer con el evento `BufferComplete`.

   ```
   bufferInfo = {}
   bufferContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_BUFFER_COMPLETE, bufferInfo, bufferContextData)
   ```

Consulte la situación de seguimiento [Reproducción de VOD con almacenamiento en búfer](/help/use-cases/tracking-scenarios/vod-buffering.md) para obtener más información.
