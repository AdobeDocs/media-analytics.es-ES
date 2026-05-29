---
title: Seguimiento de reproducción de contenido
description: Obtenga información acerca del seguimiento de la reproducción principal, incluido el seguimiento de la carga, el inicio, la pausa y la finalización de los contenidos.
uuid: 7b8e2f76-bc4e-4721-8933-3e4453b01788
exl-id: 98ad2783-c9e3-48de-88df-8549f26114a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/cHrkCe0mQm8GlHwLVgf4cjF0VM8B1r3CRt39I2LB6kk
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: e7d92df1-c5ba-4e93-85df-f83171b889beid: e992d880-33bc-4949-a648-aa7d410276cd
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 803
ht-degree: 2%

---


# Seguimiento de reproducción de contenido

El seguimiento de reproducción principal abarca la carga de medios, el inicio, la pausa, la reanudación, la finalización y el final de sesión. Aunque no es obligatorio, el almacenamiento en búfer y la búsqueda de seguimiento también son componentes principales de una implementación de reproducción completa.

## Eventos del reproductor

| Evento del reproductor | Acción |
| --- | --- |
| Carga de medios | Crear objeto de medios; llamar a SessionStart |
| Inicio de medios | Llamar a reproducción |
| Pausa | Llamar a PauseStart |
| Reanudar tras la pausa | Llamar a reproducción |
| Medios completados | Invocar a SessionComplete |
| Anulación/descarga de contenido | Llamar a SessionEnd |
| Inicio del almacenamiento en búfer | Inicio del búfer de llamadas |
| Finaliza el almacenamiento en búfer | Llamar a reproducción (reanudar) |
| La búsqueda comienza | Invocar a SeekStart |
| Buscar finales | Llame a SeekComplete, y después a Play |

## Pasos de implementación

1. **Identificar cuándo el usuario déclencheur la reproducción** (el usuario hace clic en reproducir o la reproducción automática se activa). Cree un objeto de medios con nombre de contenido, ID, longitud, tipo de flujo y tipo de medios. Consulte [Nombre de contenido](/help/implementation/variables/core/content-name.md), [ID de contenido](/help/implementation/variables/core/content-id.md), [Longitud del contenido](/help/implementation/variables/core/content-length.md), [Tipo de emisión](/help/implementation/variables/core/stream-type.md) y [Tipo de contenido](/help/implementation/variables/core/content-type.md) para ver las definiciones de los campos.
1. **Opcionalmente, se pueden adjuntar metadatos** — metadatos estándar (programa, temporada, episodio, etc.) y variables de datos de contexto personalizadas. Consulte [Programa](/help/implementation/variables/standard-metadata/show.md), [Temporada](/help/implementation/variables/standard-metadata/season.md), [Episodio](/help/implementation/variables/standard-metadata/episode.md), [Género](/help/implementation/variables/standard-metadata/genre.md) y [Red](/help/implementation/variables/standard-metadata/network.md) para ver las referencias de claves de metadatos estándar.
1. **Llame a [Inicio de sesión](/help/implementation/events/session/session-start.md)** para iniciar el seguimiento de la sesión. Esto carga los datos y los metadatos e inicia la medición de QoS (tiempo de inicio). SessionStart hace un seguimiento de *Intent* para reproducir, no el primer fotograma.
1. **Llamar a [Reproducir](/help/implementation/events/playback/play.md)** cuando el primer fotograma de contenido aparece en pantalla.
1. **Invocar a [Pausar inicio](/help/implementation/events/playback/pause-start.md)** cuando el reproductor se detenga. Vuelva a llamar a Reproducir cuando se reanude la reproducción. No hay ningún evento de reanudación independiente.
1. **Invocar a [sesión completada](/help/implementation/events/session/session-complete.md)** cuando el visor llegue al final del contenido.
1. **Invocar a [Fin de sesión](/help/implementation/events/session/session-end.md)** cuando se descargue el reproductor o el visor abandone el contenido sin llegar al final. SessionEnd cierra inmediatamente la sesión; no se puede realizar un seguimiento de más eventos después de ella.

>[!IMPORTANT]
>
>`SessionEnd` marca el final de una sesión de seguimiento. Si la sesión se vio por completo correctamente, llame a `SessionComplete` antes de `SessionEnd`. Se omite cualquier otra llamada de seguimiento después de `SessionEnd`, excepto `SessionStart` para una nueva sesión.

## Reproducción principal

Los siguientes ejemplos muestran un flujo de sesión completo, desde el inicio de la sesión hasta la finalización del contenido y el final de la sesión.

Para obtener detalles de implementación por plataforma, consulte [Inicio de sesión](/help/implementation/events/session/session-start.md), [Reproducir](/help/implementation/events/playback/play.md), [Pausar inicio](/help/implementation/events/playback/pause-start.md), [Sesión completa](/help/implementation/events/session/session-complete.md) y [Fin de sesión](/help/implementation/events/session/session-end.md).

## Almacenamiento en búfer

El inicio del búfer indica que el reproductor está esperando datos. El final del búfer se infiere al enviar un evento de reproducción después de BufferStart (API basadas en XDM). En Mobile SDK, llame también explícitamente a BufferComplete.

Para obtener detalles de implementación, consulte [Inicio del búfer](/help/implementation/events/playback/buffer-start.md).

## Buscando

Las señales de inicio de búsqueda indican que el usuario está borrando. La función de búsqueda final va seguida de Reproducción para reanudar la reproducción del contenido.

Para obtener detalles de implementación, vea [Pausar inicio](/help/implementation/events/playback/pause-start.md) (inicio de búsqueda) y [Reproducir](/help/implementation/events/playback/play.md) (fin de búsqueda).

## Gestión de interrupciones de aplicaciones

La reproducción en una aplicación multimedia se puede interrumpir de varias formas: el usuario hace una pausa, la aplicación se pone en segundo plano y se produce una llamada telefónica. Independientemente de la causa, las instrucciones de seguimiento son las mismas:

1. Invoque **PauseStart** cuando la aplicación se interrumpa (se pone en segundo plano, se pausa el contenido, etc.).
1. Invoque **Play** cuando la aplicación vuelva a estar en primer plano o cuando se reanude la reproducción de contenido.

>[!NOTE]
>
>No llame a SessionStart cuando la aplicación vuelva al primer plano. La llamada a SessionStart hace que la reproducción hasta ese punto no se cuente hasta el tiempo total de reproducción y que se pierdan los marcadores de progreso, segmentos y límites de capítulo anteriores.

**¿Cuándo debe finalizar una sesión en pausa?** Si la aplicación no permite la reproducción en segundo plano, llame a PauseStart inmediatamente y, a continuación, a SessionEnd después de aproximadamente un minuto en segundo plano. La aplicación no puede continuar enviando pings de pausa desde segundo plano y mantener la sesión abierta indefinidamente proporciona una mala experiencia. Si la aplicación admite la reproducción en segundo plano (aplicaciones de audio y de podcast de vídeo), siga enviando pings mientras está en segundo plano.

**Reinicio después de un largo período de tiempo en segundo plano:** Si la aplicación se puso en segundo plano el tiempo suficiente para que la sesión caducara (inactividad de 30 minutos), llame a SessionEnd para cerrar sin problemas cualquier sesión persistente y, a continuación, llame a SessionStart para comenzar una nueva cuando regrese el visor.

## Reanudación de sesiones inactivas

Una sesión caduca automáticamente si no se reciben eventos durante 10 minutos o si no hay movimiento del cabezal de reproducción durante 30 minutos. Si el usuario vuelve después de que haya caducado una sesión, vuelva a llamar a SessionStart para abrir una nueva sesión.

**Reanudación entre dispositivos (transferencia entre dispositivos):** Cuando un visor transfiera la reproducción entre dispositivos (por ejemplo, pasar de un teléfono a un televisor), use el indicador de reanudación para unir las sesiones en los informes de Analytics:

1. En el **dispositivo de origen**, llame a SessionEnd cuando el visor inicie la conversión. No llamar a SessionComplete: el contenido no ha finalizado.
1. En el **dispositivo de destino**, llame a SessionStart con el indicador de reanudación establecido en `true` y pase los mismos metadatos de contenido y la posición del cabezal de reproducción desde el dispositivo de origen.

Si se establece el indicador de reanudación, Analytics incrementará [las reanudaciones de contenido](/help/reporting/metrics/content-resumes.md) en lugar de [los inicios de medios](/help/reporting/metrics/media-starts.md) en la segunda parte del envío.

**Reanudar manualmente una sesión previamente cerrada:** Si la aplicación almacena datos de usuario y puede reanudar una sesión previamente cerrada, establezca el indicador de reanudación al inicio de la sesión. Consulte [Inicio de sesión](/help/implementation/events/session/session-start.md#resuming-a-session) para obtener detalles de implementación en todas las plataformas.
