---
title: Resumen de eventos de medios de streaming
description: Obtenga información acerca de los tipos de eventos de medios y el orden en que deben enviarse.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---


# Eventos de medios de streaming

El seguimiento de medios de streaming funciona enviando una secuencia de llamadas de evento a un extremo de recopilación de datos de Adobe, cada una de las cuales representa una transición en el estado del reproductor. Cada evento pertenece a una sesión activa abierta por una llamada de [inicio de sesión](session/session-start.md). Las sesiones se cierran automáticamente por expiración o pueden cerrarse inmediatamente con una llamada de [Fin de sesión](session/session-end.md).

Los eventos se agrupan en seis categorías (sesión, reproducción, anuncios, capítulos, estado del reproductor y calidad), cada una de las cuales cubre un aspecto distinto de la experiencia multimedia.

## Eventos de sesión

Los eventos de sesión se aplican a cualquier tipo de seguimiento de medios, incluidos vídeo bajo demanda, emisiones en directo, podcasts y audiolibros. Definen los límites de la propia sesión de seguimiento. El evento de sesión más importante es [Inicio de sesión](session/session-start.md), ya que casi todos los demás tipos de evento dependen del ID de sesión que genere. Mándelo como el primer evento cuando un usuario inicia una sesión, como cuando pulsa reproducir o cuando el reproductor comienza la reproducción automática.

Una vez que se abra una sesión, use [Sesión completada](session/session-complete.md) o [Fin de sesión](session/session-end.md) para indicar cómo terminó la experiencia de visualización. Enviar sesión completa cuando el espectador llega al final natural del contenido (el vídeo termina, el episodio del podcast termina o el capítulo final de un audiolibro finaliza). La sesión completa no cierra la sesión; permanece abierta hasta que caduca de forma natural, por lo que los eventos finales, como un ping final, se seguirán capturando.

Si el visor se va antes de llegar al final, envíe [Fin de sesión](session/session-end.md) para cerrar la sesión inmediatamente. Envíe únicamente el final de la sesión cuando no se produzcan eventos adicionales (por ejemplo, cuando se destruya el reproductor o se descargue la página). El final de la sesión es un cierre grave: una vez enviada, la sesión finaliza y no se pueden rastrear más eventos debajo de ella. En la mayoría de los casos, es más seguro permitir que la sesión caduque de forma natural. Algunos ejemplos son que el visor se detiene indefinidamente, la aplicación se pone en segundo plano o el contenido no se carga.

Las sesiones caducan automáticamente si no se reciben eventos durante 10 minutos o si no se detecta ningún movimiento del cabezal de reproducción durante 30 minutos. Si se cumple cualquiera de las condiciones y el visor vuelve al contenido, debe volver a llamar a Inicio de sesión para abrir una nueva sesión antes de enviar más eventos.

## Eventos de reproducción

Los eventos de reproducción rastrean las transiciones de estado en el reproductor de contenidos a lo largo de una sesión. Constituyen el núcleo del flujo de eventos y se aplican a cualquier tipo de contenido.

El evento de reproducción principal es [Play](playback/play.md). Después de invocar a Inicio de sesión, Reproducir indica que el contenido ha comenzado a reproducirse, ya sea el inicio inicial, un déclencheur de reproducción automática o cualquier retorno al estado de reproducción. [Pausar inicio](playback/pause-start.md) indica que el usuario ha pausado la reproducción. No hay ningún evento de reanudación dedicado; cuando el visor se reanude, envíe Reproducir de nuevo. Reproducir funciona de la misma manera después de una detención del almacenamiento en búfer; enviar [Inicio del almacenamiento en búfer](playback/buffer-start.md) cuando el reproductor se detenga a la espera de datos y, a continuación, seguir con Reproducir cuando se resuelva el almacenamiento en búfer.

Envíe [Ping](playback/ping.md) cada 10 segundos durante la reproducción del contenido principal y cada 1 segundo durante la reproducción del anuncio. Ping mantiene viva la sesión y registra el movimiento del cabezal de reproducción. En los SDK móviles, los pings se envían automáticamente; en todas las demás plataformas deben enviarse manualmente.

Envíe [cambio de velocidad de bits](playback/bitrate-change.md) cada vez que el algoritmo de velocidad de bits adaptable del reproductor cambie a un nivel de calidad diferente. Si se incluye el nuevo valor de velocidad de bits en los datos de QoE, se pueden generar informes de velocidad de bits media.

## Eventos de publicidad

Los eventos de publicidad hacen un seguimiento de la publicidad dentro de una sesión multimedia. Entre las situaciones habituales se incluyen los anuncios previos a la emisión de un vídeo, los anuncios durante la emisión de un vídeo de formato largo o en directo insertados a intervalos, y los anuncios posteriores a la emisión una vez finalizado el contenido. Una sola pausa publicitaria puede contener uno o varios anuncios individuales.

Cada pausa publicitaria sigue la misma estructura. [Inicio de la pausa publicitaria](ads/ad-break-start.md) abre la pausa publicitaria y [Finalización de la pausa publicitaria](ads/ad-break-complete.md) la cierra. Estos dos eventos actúan como bookends que envuelven todos los eventos de publicidad individuales. Dentro del descanso, envía [Inicio del anuncio](ads/ad-start.md) cuando comience a reproducirse cada anuncio individual. Síguelo con [Anuncio completado](ads/ad-complete.md) si el anuncio se reproduce a toda su longitud, o [Omisión de anuncio](ads/ad-skip.md) si el visor selecciona el botón de omitir. Al omitir cualquiera de los dos bookend, se ignoran todos los eventos de anuncio de la pausa y la duración de la publicidad se atribuye incorrectamente al contenido principal.

El siguiente ejemplo muestra la secuencia de evento correcta para una sola pausa publicitaria que contiene tres anuncios, en la que el visor omitió el tercero:

1. Inicio de pausa publicitaria
2. Inicio del anuncio
3. Anuncio completado
4. Inicio del anuncio
5. Anuncio completado
6. Inicio del anuncio
7. Omisión de publicidad
8. Pausa publicitaria completa

## Eventos de capítulo

Los eventos de capítulo son opcionales y permiten realizar un seguimiento de segmentos de contenido con nombre dentro de una sesión. Son muy adecuados para el contenido naturalmente dividido en partes discretas. Algunos ejemplos comunes son capítulos de un audiolibro, actos en un documental, lecciones en un curso de vídeo o segmentos en un episodio de podcast. Utilice eventos de capítulo cuando desee comprender la participación del visualizador en el nivel de segmento, como identificar qué capítulos tienden a omitir las audiencias.

Enviar [inicio de capítulo](chapters/chapter-start.md) cuando comience un capítulo. Si el visor observa hasta el final del capítulo, envíe [Capítulo completado](chapters/chapter-complete.md). Si el visor busca más allá del límite del capítulo sin verlo hasta su finalización, envíe [omitir capítulo](chapters/chapter-skip.md) en su lugar. Un capítulo debe cerrarse con Capítulo completado u Capítulo omitido antes de que se pueda abrir uno nuevo; los capítulos no pueden superponerse.

## Eventos de estado del reproductor

Los eventos de estado del reproductor rastrean cómo los visualizadores interactúan con los controles del reproductor a lo largo de una sesión. Son útiles para comprender el uso de las funciones de accesibilidad, como la frecuencia con la que los visualizadores habilitan los subtítulos o el silencio. También revelan patrones de comportamiento de visualización como la pantalla completa frente a la visualización en línea y la multitarea de imagen en imagen.

Los cinco estados a los que se puede realizar el seguimiento son: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture` y `inFocus`. Envíe [Inicio de estado](player-state/state-start.md) cuando el reproductor entre en cualquiera de estos estados y [Fin de estado](player-state/state-end.md) cuando salga. Se pueden activar varios estados al mismo tiempo; un visualizador puede estar en pantalla completa y silenciarse simultáneamente, y se pueden finalizar varios estados dentro de la misma llamada de evento.

## Eventos de error

El evento [Error](error.md) registra un error de reproducción durante una sesión: una solicitud de flujo fallida, un error de códec o un error de envío externo. Enviarlo siempre que se produzca un error significativo. Un evento de error no cierra la sesión; la reproducción puede continuar y los eventos posteriores se rastrean en la misma sesión. Si el error no se puede recuperar, sígalo con Fin de sesión para cerrar explícitamente la sesión.

>[!MORELIKETHIS]
>
>* [Resumen de variables](/help/implementation/variables/overview.md): Los datos que los eventos llevan a Adobe
>* [Resumen de dimensiones](/help/reporting/dimensions/overview.md): Las dimensiones de informes que rellenan los eventos
>* [Resumen de métricas](/help/reporting/metrics/overview.md): Las métricas de informes que rellenan los eventos
