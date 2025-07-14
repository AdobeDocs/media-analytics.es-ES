---
title: Obtenga información sobre cómo migrar de Milestone a Media Analytics
description: Aprenda a cambiar variables de Milestone por métricas de Media Analytics, y métodos del módulo Milestone por sintaxis de Media Analytics.
uuid: fdc96146-af63-48ce-b938-c0ca70729277
exl-id: 655841ed-3a02-4e33-bbc9-46fb14302194
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 96%

---

# Migración de Milestone a Media Analytics {#migrating-from-milestone-to-media-analytics}

## Información general   {#overview}

Los conceptos principales de la medición de vídeo son los mismos para Milestone y Media Analytics, que lleva eventos de reproductor de vídeo y los asigna a métodos de análisis, al tiempo que toma metadatos y valores del reproductor y los asigna a variables de análisis. La solución de Media Analytics se desarrolló a partir de Milestone, por lo que muchos de los métodos y métricas son los mismos; sin embargo, el enfoque de configuración y el código han cambiado significativamente. Debería ser posible actualizar el código de evento del reproductor para que indique los nuevos métodos de Media Analytics. Consulte [Información general de SDK](/help/legacy/setup/legacy-setup-overview.md) e [Información general del seguimiento](/help/use-cases/track-av-playback/track-core-overview.md) para obtener más información sobre la implementación de Media Analytics.

En las tablas siguientes se proporcionan las correspondencias entre la solución Milestone y la solución Media Analytics.

## Guía de migración {#migration-guide}

### Referencia de variable

| Métrica de Milestone | Tipo de variable | Métrica de Media Analytics |
| --- | --- | --- |
| Contenido | <br>Caducidad predeterminada de la eVar: Visita | Contenido |
| Tipo de contenido | <br>Caducidad predeterminada de la eVar: Vista de página | Tipo de contenido |
| Tiempo invertido en contenido | Tipo de evento: <br>Contador | Tiempo invertido en contenido |
| Inicios de vídeo | Tipo de evento: <br>Contador | Inicios de vídeo |
| Vídeos completados | Tipo de evento: <br>Contador | Contenido finalizado |


### Variables de módulo multimedia

| Milestone | Sintaxis de Milestone | Media Analytics | Sintaxis de Media Analytics |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | N/D | Todos los datos de Media Analytics solo se envían mediante datos de contexto. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/D | Los datos de contexto de Media Analytics se rellenan automáticamente en las variables reservadas. Ya no es necesario asignar eVars, props y eventos en el código de implementación. Los clientes pueden asignar datos de contexto a variables mediante el uso de reglas de procesamiento. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | N/D | Ya no es necesario puesto que se realiza mediante variables reservadas y reglas de procesamiento. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | N/D | Ya no es necesario puesto que se realiza mediante variables reservadas y reglas de procesamiento. |

### Variables opcionales

| Milestone | Sintaxis de Milestone | Media Analytics | Sintaxis de Media Analytics |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/D | Ya no proporcionamos asignaciones de reproductor precompiladas. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/D | Ya no proporcionamos asignaciones de reproductor precompiladas. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/D | La finalización del contenido solo admite un marcador de progreso del 100%. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/D | La finalización del contenido solo admite un marcador de progreso del 100%. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Clave de SDK: playerName;<br> Clave de API: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/D | Media Analytics tiene establecido 10 segundos para el contenido y 1 segundo para los anuncios. No hay más opciones disponibles. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/D | Media Analytics siempre realiza un seguimiento de los marcadores de progreso en el 10 %, 25 %, 50 %, 75 % y 95 %. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media Analytics siempre realiza un seguimiento de los marcadores de progreso en el 10 %, 25 %, 50 %, 75 % y 95 %. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/D | El seguimiento automático ya no está disponible. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/D | El seguimiento automático ya no está disponible. |

### Variables de seguimiento de anuncios

| Milestone | Sintaxis de Milestone | Media Analytics | Sintaxis de Media Analytics |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/D | Media Analytics tiene establecido 10 segundos para el contenido y 1 segundo para los anuncios. No hay más opciones disponibles. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/D | Los marcadores de progreso no se proporcionan de forma predeterminada para las publicidades. Utilice métricas calculadas para crear marcadores de progreso de anuncios. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media Analytics se establece en 1 segundo para las publicidades. No hay más opciones disponibles. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/D | El seguimiento automático ya no está disponible. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/D | El seguimiento automático ya no está disponible. |

### Métodos de módulo multimedia

| Milestone | Sintaxis de Milestone | Media Analytics | Sintaxis de Media Analytics |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName | `mediaName`: (requerido) nombre del vídeo tal como desea que aparezca en informes de vídeo. | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength | `mediaLength`: (requerido) duración del vídeo en segundos. | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName | `mediaPlayerName`: (requerido) nombre del reproductor multimedia que se utilizó para ver el vídeo, tal como desea que aparezca en informes de vídeo. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name | `name`: (requerido) nombre o ID del anuncio. | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length | `length`: (requerido) duración del anuncio. | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName | `playerName`: (requerido) nombre del reproductor de contenidos que se utilizó para ver el anuncio. | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName | `parentName`: Nombre o ID del contenido primario donde está incrustado el anuncio. | N/D | Heredado automáticamente. |
| parentPod | `parentPod`: Posición en el contenido primario en que se reprodujo el anuncio. | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition | `parentPodPosition`: Posición dentro del pod donde se reproduce el anuncio. | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM | `CPM`: CPM o CPM cifrado (con el prefijo “~”) que se aplica a esta reproducción. | N/D | No disponible de forma predeterminada en Media Analytics. |
| Media.click | `s.Media.click(name, offset)` | N/D | Utilice una llamada de análisis de vínculo personalizado para hacer un seguimiento de los clics. |
| Media.close | `s.Media.close(mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(name, offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(mediaName, mediaOffset)` | trackPause<br> o <br>trackEvent | `trackPause()` <br> O bien `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> O bien <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Utilice metadatos personalizados o estándar para establecer variables adicionales. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(mediaName)` | N/D | La frecuencia de llamada de seguimiento se configura automáticamente. |
