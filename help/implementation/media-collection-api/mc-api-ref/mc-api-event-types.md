---
title: Tipos y descripciones de eventos de medios de transmisión
description: '¿Cuáles son los tipos y descripciones de los eventos de recopilación de medios? '
uuid: bc4f75a7-ea22-47eb-a50d-5f41274c6d41
exl-id: f2919e69-8b03-45b4-b9cd-365222a061e0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 98722998606af3761652e282c31338bb966eb654
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 79%

---

# Tipos de eventos y descripciones{#event-types-and-descriptions}

## sessionStart

Enviado con la llamada `sessions`. Cuando reciba la respuesta, extraiga el ID de sesión del encabezado Ubicación y utilícelo para las llamadas de evento subsiguientes al servidor de recopilación.

## play

Se envía cuando el reproductor cambia de estado a “reproduciendo” (es decir, la función de llamada de retorno `on('Playing')` se activa en el reproductor). Otros estados desde los que el reproductor se desplaza a &quot;reproduciendo&quot; incluyen &quot;almacenamiento en búfer&quot;, seguir desde &quot;en pausa&quot;, recuperación de un error, reproducción automática, etc.

## ping

* **Contenido principal:** Debe enviarse cada 10 segundos durante la reproducción del contenido principal, independientemente de los demás eventos de API que se hayan enviado. El primer evento de ping debe activarse 10 segundos después de iniciarse la reproducción del contenido principal.
* **Contenido de la publicidad:** Debe enviarse cada 1 segundo durante el seguimiento de la publicidad.

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

Si no se envía un(a) `sessionEnd`, una sesión abandonada [se agotará el tiempo de espera de forma normal](../mc-api-impl/mc-api-timeout.md) (después de que no se reciba ningún evento durante 10 minutos o cuando no se produzca ningún movimiento del cabezal de reproducción durante 30 minutos). Además, se perderán todas las llamadas de medios subsiguientes realizadas con ese ID de sesión.

## sessionComplete

Se envía cuando se llega al final del contenido principal.

>[!IMPORTANT]
>
>Debe hacer referencia a los [esquemas de validación de JSON](mc-api-json-validation.md) para cada tipo de evento y comprobar los requisitos y tipos de parámetros de eventos correctos.

## stateStart

Indica el inicio del seguimiento del estado del reproductor.

Para obtener más información, consulte [Implementación y sistema de informes](/help/use-cases/player-state-tracking/implementation-and-reporting.md).

## stateEnd

Indica el final del seguimiento del estado del reproductor.

Para obtener más información, consulte [Implementación y sistema de informes](/help/use-cases/player-state-tracking/implementation-and-reporting.md).
