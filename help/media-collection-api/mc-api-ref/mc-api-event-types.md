---
seo-title: Tipos de eventos y descripciones
title: Tipos de eventos y descripciones
uuid: bc 4 f 75 a 7-ea 22-47 eb-a 50 d -5 f 41274 c 6 d 41
translation-type: tm+mt
source-git-commit: 69057b2abf7140d52b1897af3dc9d9fd01ca87ad

---


# Tipos de eventos y descripciones{#event-types-and-descriptions}

## sessionStart

Sent with the `sessions` call. Cuando reciba la respuesta, extraiga el ID de sesión del encabezado Ubicación y utilícelo para las llamadas de evento subsiguientes al servidor de recopilación.

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). Otros estados desde los que el reproductor se desplaza a "reproduciendo" incluyen "almacenamiento en búfer", seguir desde "en pausa", recuperación de un error, reproducción automática, etc.

## ping

* **Contenido principal**: se debe enviar cada 10 segundos durante la reproducción del contenido principal, independientemente de los demás eventos de API que se hayan enviado. El primer evento de ping debe activarse 10 segundos después de iniciarse la reproducción del contenido principal.
* **Contenido de publicidad**: se debe enviar cada segundo durante el seguimiento de publicidad.

Los eventos ping *no* deben incluir el mapa de `params` en el cuerpo de la solicitud.

## Bitratechange

Se envía cuando cambia la velocidad de bits.

## bufferStart

Se envía cuando se inicia el almacenamiento en búfer. No hay ningún tipo de evento `bufferResume`. A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## pauseStart

Se envía cuando el usuario pulsa Pausa. No hay ningún tipo de evento `resume`. A `resume` is inferred when you send a `play` event after a `pauseStart`.

## adBreakStart

Indica el comienzo de una pausa publicitaria

## adStart

Indica el inicio de una publicidad

## adComplete

Indica la finalización de una pausa publicitaria

## adSkip

Indica un skip de publicidad

## adBreakComplete

Indica la finalización de una pausa publicitaria

## chapterStart

Indica el comienzo de un segmento de capítulo

## chapterSkip

Indica un skip de capítulo

## chapterComplete

Indica la finalización de un capítulo

## error

Indica que se produjo un error.

## sessionEnd

Se utiliza para notificar al servidor de Media Analytics cómo cerrar la sesión inmediatamente cuando el usuario abandonó su visualización del contenido y es poco probable que se devuelva.

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## sessionComplete

Se envía cuando se llega al final del contenido principal

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](../../media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.

