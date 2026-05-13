---
title: Cómo rastrear la reproducción principal en Chromecast
description: Obtenga información sobre cómo rastrear eventos de almacenamiento en búfer en Chromecast.
uuid: f6fa3a1a-d7de-4293-bd11-ebe9e130badd
exl-id: 26fd1e2a-4103-486f-be12-36b088d28cb6
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/zIbnO6-BkK6uxr7-wdIzog76FsVtqFatq-RFu-PjHiI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 142
ht-degree: 100%

---

# Seguimiento del almacenamiento en búfer en Chromecast{#track-buffering-on-chromecast}

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

1. Escuche los eventos de almacenamiento en búfer de reproducción procedentes del reproductor de medios y, cuando reciba la notificación del evento Inicio de almacenamiento en búfer, rastree el almacenamiento en búfer mediante el evento `BufferStart`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent).

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);
   ```

1. En la notificación de Finalización de almacenamiento en búfer procedente del reproductor de medios, rastree el final del almacenamiento en búfer con el evento `BufferComplete`: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent).

   ```js
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
   ```

Consulte la situación de seguimiento [Reproducción de VOD con almacenamiento en búfer](/help/use-cases/tracking-scenarios/vod-buffering.md) para obtener más información.
