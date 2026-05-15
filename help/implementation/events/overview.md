---
title: Resumen de eventos de medios de streaming
description: Obtenga información acerca de los tipos de eventos de medios y el orden en que deben enviarse.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 4%

---


# Eventos de medios de streaming

El seguimiento de medios de streaming funciona enviando una secuencia de llamadas de evento, cada una de las cuales representa una transición de estado del reproductor, a un punto final de recopilación de datos de Adobe. Cada evento pertenece a una sesión activa que comienza con una llamada de [sessionStart](session/session-start.md) y se cierra con [sessionComplete](session/session-complete.md) o [sessionEnd](session/session-end.md).

## Flujo de trabajo de eventos

La siguiente lista ordenada muestra la secuencia de eventos necesaria para una reproducción típica de VOD con un anuncio previo a la emisión y un capítulo:

1. **[Inicio de sesión](session/session-start.md)**: Siempre es el primer evento; crea la sesión y devuelve un ID de sesión
2. **[Inicio de la pausa publicitaria](ads/ad-break-start.md)**: obligatorio antes de cualquier evento publicitario
3. **[Inicio del anuncio](ads/ad-start.md)** → **[Finalización del anuncio](ads/ad-complete.md)** (o **[Omisión del anuncio](ads/ad-skip.md)**)
4. **[Se completó la pausa publicitaria](ads/ad-break-complete.md)**: Necesario después de todos los anuncios de la pausa
5. **[Reproducir](playback/play.md)**: indica que el contenido comienza o se reanuda
6. **[Inicio del capítulo](chapters/chapter-start.md)**: Opcional; marca el comienzo de un capítulo
7. **[Ping](playback/ping.md)**: enviado cada 10 segundos durante el contenido principal, cada 1 segundo durante los anuncios
8. **[Capítulo completado](chapters/chapter-complete.md)**: Opcional; marca el final de un capítulo
9. **[Pausar inicio](playback/pause-start.md)** → **[Reproducir](playback/play.md)** (reanudar): Para cualquier pausa
10. **[Inicio del búfer](playback/buffer-start.md)** → **[Reproducir](playback/play.md)** (reanudar): Para cualquier almacenamiento en búfer
11. **[Sesión completa](session/session-complete.md)**: Cuando el visor llega al final del contenido

Utilice [Fin de sesión](session/session-end.md) en lugar de Sesión completa si el visor abandona la sesión antes de llegar al final del contenido.

## Ciclo de sesión

Las sesiones caducan automáticamente si se cumple cualquiera de las siguientes condiciones:

* No se reciben eventos durante **10 minutos**
* No hubo movimiento del cabezal de reproducción durante **30 minutos**

## Referencia de evento

| Evento | Categoría | Métrica asociada |
| --- | --- | --- |
| [Inicio de sesión](session/session-start.md) | Sesión | [Comienzos de medios](/help/reporting/metrics/media-starts.md) |
| [Sesión completa](session/session-complete.md) | Sesión | [Contenido finalizado](/help/reporting/metrics/content-completes.md) |
| [Fin de sesión](session/session-end.md) | Sesión | — |
| [Reproducir](playback/play.md) | Reproducción | [El contenido comienza](/help/reporting/metrics/content-starts.md) |
| [Pausar inicio](playback/pause-start.md) | Reproducción | [Pausar eventos](/help/reporting/metrics/pause-events.md) |
| [Inicio del búfer](playback/buffer-start.md) | Reproducción | [Eventos de búfer](/help/reporting/metrics/buffer-events.md) |
| [Cambio de velocidad de bits](playback/bitrate-change.md) | Reproducción | [Cambios de velocidad de bits](/help/reporting/metrics/bitrate-changes.md) |
| [Ping](playback/ping.md) | Reproducción | — |
| [Inicio de la pausa publicitaria](ads/ad-break-start.md) | Anuncios | — |
| [Inicio del anuncio](ads/ad-start.md) | Anuncios | [El anuncio comienza](/help/reporting/metrics/ad-starts.md) |
| [Anuncio completado](ads/ad-complete.md) | Anuncios | [Finalización del anuncio](/help/reporting/metrics/ad-completes.md) |
| [Omisión de publicidad](ads/ad-skip.md) | Anuncios | — |
| [Se completó la pausa publicitaria](ads/ad-break-complete.md) | Anuncios | — |
| [Inicio del capítulo](chapters/chapter-start.md) | Capítulos | [El capítulo comienza](/help/reporting/metrics/chapter-starts.md) |
| [Capítulo completado](chapters/chapter-complete.md) | Capítulos | [El capítulo finaliza](/help/reporting/metrics/chapter-completes.md) |
| [Omisión de capítulo](chapters/chapter-skip.md) | Capítulos | — |
| [Inicio de estado](player-state/state-start.md) | Estado del reproductor | Varía por estado |
| [Fin de estado](player-state/state-end.md) | Estado del reproductor | Varía por estado |
| [Error](error.md) | Calidad | [Flujos afectados por error](/help/reporting/metrics/error-impacted-streams.md) |

>[!MORELIKETHIS]
>
>* [Esquemas de validación de JSON](/help/implementation/media-collection-api/mc-api-ref/mc-api-json-validation.md): compruebe la estructura de carga útil de la solicitud para cada tipo de evento
>* [Extremo de solicitud de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md): referencia de extremo de API de recopilación de medios
>* [Extremo de solicitud de sesiones](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md): cree una sesión antes de enviar eventos
>* [Seguimiento del estado del reproductor](/help/use-cases/player-state-tracking/implementation-and-reporting.md): Detalles de implementación de inicio y fin de estado
