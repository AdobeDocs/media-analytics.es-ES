---
seo-title: Tipos de eventos y descripciones
title: Tipos de eventos y descripciones
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Tipos de eventos y descripciones{#event-types-and-descriptions}

## sessionStart

Enviado con la `sessions` llamada. Cuando reciba la respuesta, extraiga el ID de sesión del encabezado Ubicación y utilícelo para las llamadas de evento subsiguientes al servidor de recopilación.

## play

Sent when the player changes state to "playing" from another state (i.e., the `on('Playing')` callback is triggered by the player). Otros estados desde los que el reproductor se desplaza a "reproduciendo" incluyen "almacenamiento en búfer", seguir desde "en pausa", recuperación de un error, reproducción automática, etc.

## ping

* **Contenido principal**: se debe enviar cada 10 segundos durante la reproducción del contenido principal, independientemente de los demás eventos de API que se hayan enviado. El primer evento de ping debe activarse 10 segundos después de iniciarse la reproducción del contenido principal.
* **Contenido de publicidad**: se debe enviar cada segundo durante el seguimiento de publicidad.

Los eventos ping *no* deben incluir el mapa de `params` en el cuerpo de la solicitud.

## bitrateChange

Sent when the bitrage changes.

## bufferStart

Sent when buffering starts. No hay ningún tipo de evento `bufferResume`. A `bufferResume` is inferred when you send a `play` event after `bufferStart`.

## pauseStart

Se envía cuando el usuario pulsa Pausa. No hay ningún tipo de evento `resume`. A `resume` is inferred when you send a `play` event after a `pauseStart`.

## adBreakStart

Indica el inicio de una pausa publicitaria

## adStart

Indica el inicio de una publicidad

## adComplete

Signals the completion of an ad break

## adSkip

Indica un salto de publicidad

## adBreakComplete

Indica la finalización de una pausa publicitaria

## chapterStart

Indica el inicio de un segmento de capítulo

## chapterSkip

Indica un salto de capítulo

## chapterComplete

Indica la finalización de un capítulo

## error

Indica que se ha producido un error.

## sessionEnd

This is used to notify the Media Analytics backend to immediately close the session when the user has abandoned their viewing of the content and they are unlikely to return.

If you don't send a `sessionEnd`, an abandoned session will time-out normally (after no events are received for 10 minutes, or when no playhead movement occurs for 30 minutes), and the session is deleted by the backend.

## sessionComplete

Se envía cuando se llega al final del contenido principal

>[!IMPORTANT]
>
>You should refer to the [JSON validation schemas](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) for each event type, to verify correct event parameter types and requirements.

