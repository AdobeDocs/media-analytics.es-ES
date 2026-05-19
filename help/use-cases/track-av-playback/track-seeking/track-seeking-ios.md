---
title: Aprenda a rastrear la búsqueda en iOS
description: Obtenga información sobre cómo rastrear eventos de inicio y finalización de llamada mediante Media SDK en iOS.
uuid: 1d31ae99-384f-4b4d-b557-4018db177349
exl-id: e8cb4962-2a14-4bfe-9a25-2405e503ba0b
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/JWe9oadtMZIK8INj8SJ1riBfNGIaXympyhPoyg-8umk
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 133
ht-degree: 100%

---

# Seguimiento de llamada a otro punto del contenido en iOS{#track-seeking-on-ios}

En las siguientes instrucciones se indican los pasos para la implementación en todos los kits de desarrollo de software de 2.x.

>[!IMPORTANT]
>
>Si va a implementar una versión 1.x del SDK, puede descargar las guías del desarrollador de 1.x aquí: [Descargar SDK.](/help/getting-started/download-sdks.md)

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

Consulte la situación de seguimiento [Reproducción de VOD con llamada a otro punto del contenido principal](/help/use-cases/tracking-scenarios/vod-seeking.md) para obtener más información.
