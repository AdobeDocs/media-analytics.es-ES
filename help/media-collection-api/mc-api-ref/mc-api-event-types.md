---
title: Tipos de eventos y descripciones
description: null
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Tipos de eventos y descripciones {#event-types-and-descriptions}

## sessionStart

Enviado con la llamada `sessions`. Cuando reciba la respuesta, extraiga el ID de sesión del encabezado Ubicación y utilícelo para las llamadas de evento subsiguientes al servidor de recopilación.

## play

Se envía cuando el reproductor cambia de estado a “reproduciendo” (es decir, la función de llamada de retorno `on('Playing')` se activa en el reproductor). Otros estados desde los que el reproductor se desplaza a "reproduciendo" incluyen "almacenamiento en búfer", seguir desde "en pausa", recuperación de un error, reproducción automática, etc.

## ping

* **Contenido principal**: se debe enviar cada 10 segundos durante la reproducción del contenido principal, independientemente de los demás eventos de API que se hayan enviado. El primer evento de ping debe activarse 10 segundos después de iniciarse la reproducción del contenido principal.
* **Contenido de publicidad**: se debe enviar cada segundo durante el seguimiento de publicidad.

Los eventos ping *no* deben incluir el mapa de `params` en el cuerpo de la solicitud.

## bitrateChange

Se envía cuando cambia la velocidad de bits.

## bufferStart

Se envía cuando se inicia el almacenamiento en búfer. No hay ningún tipo de evento `bufferResume`. Se infiere `bufferResume` al enviar un evento `play` después de `bufferStart`.

## pauseStart

Se envía cuando el usuario pulsa Pausa. No hay ningún tipo de evento `resume`. Se infiere `resume` al enviar un evento `play` después de `pauseStart`.

## adBreakStart

Indica el comienzo de una pausa publicitaria.

## adStart

Indica el comienzo de publicidad.

## adComplete

Indica la finalización de una pausa publicitaria.

## adSkip

Indica una omisión de publicidad.

## adBreakComplete

Indica la finalización de una pausa publicitaria.

## chapterStart

Indica el comienzo de un segmento de capítulo.

## chapterSkip

Indica una omisión de capítulo.

## chapterComplete

Indica la finalización de un capítulo.

## error

Indica que se ha producido un error.

## sessionEnd

Se utiliza para informar al backend de Media Analytics de que cierre inmediatamente la sesión cuando el usuario ha abandonado el contenido y es poco probable que vuelva.

Si no envía un `sessionEnd`, una sesión abandonada se pausará normalmente (después de que no se reciba ningún evento durante 10 minutos o cuando no se produzca ningún movimiento del cabezal de reproducción durante 30 minutos), y la sesión se eliminará en el servidor.

## sessionComplete

Se envía cuando se llega al final del contenido principal.

>[!IMPORTANT]
>
>Debe hacer referencia a los [esquemas de validación de JSON](/help/media-collection-api/mc-api-ref/mc-api-json-validation.md) para cada tipo de evento y comprobar los requisitos y tipos de parámetros de eventos correctos.

