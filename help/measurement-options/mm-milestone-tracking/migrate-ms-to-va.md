---
title: Migración de Milestone a Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: tm+mt
source-git-commit: aa2a230daa96b823f9963345ac4578799e59d3f5
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 77%

---


# Migración de Milestone a Media Analytics {#migrating-from-milestone-to-media-analytics}

## Información general {#overview}

Los conceptos principales de la medición de vídeo son los mismos para Milestone y Media Analytics, que lleva eventos de reproductor de vídeo y los asigna a métodos de análisis, al tiempo que toma metadatos y valores del reproductor y los asigna a variables de análisis. La solución de Media Analytics se desarrolló a partir de Milestone, por lo que muchos de los métodos y métricas son los mismos; sin embargo, el enfoque de configuración y el código han cambiado significativamente. Debería ser posible actualizar el código de evento del reproductor para que indique los nuevos métodos de Media Analytics. Consulte [Información general de SDK](/help/sdk-implement/setup/setup-overview.md) e [Información general del seguimiento](/help/sdk-implement/track-av-playback/track-core-overview.md) para obtener más información sobre la implementación de Media Analytics.

En las tablas siguientes se proporcionan las correspondencias entre la solución Milestone y la solución Media Analytics.

## Guía de migración {#migration-guide}

### Referencia de variable

| Métrica de Milestone | Tipo de variable | Métrica de Media Analytics |
| --- | --- | --- |
| Contenido | <br>Caducidad predeterminada de la eVar: Visita | Contenido |
| Tipo de contenido | <br>Caducidad predeterminada de la eVar: Vista de página | Tipo de contenido |
| Tiempo invertido en contenido | Tipo de evento<br>: Contador | Tiempo invertido en contenido |
| Inicios de vídeo | Tipo de evento<br>: Contador | Inicios de vídeo |
| Vídeos completados | Tipo de evento<br>: Contador | Contenido finalizado |

### Variables de módulo multimedia

| Milestone | Sintaxis de Milestone | Media Analytics | Sintaxis de Media Analytics |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | N/D | Todos los datos de Media Analytics solo se envían mediante datos de contexto. |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/A | Los datos de contexto de Media Analytics se rellenan automáticamente en las variables reservadas. Ya no es necesario asignar eVars, props y eventos en el código de implementación. Los clientes pueden asignar datos de contexto a variables mediante el uso de reglas de procesamiento. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | N/A | Ya no es necesario puesto que se realiza mediante variables reservadas y reglas de procesamiento. |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | N/A | Ya no es necesario puesto que se realiza mediante variables reservadas y reglas de procesamiento. |

### Variables opcionales

| Milestone | Sintaxis de Milestone | Media Analytics | Sintaxis de Media Analytics |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/D | Ya no proporcionamos asignaciones de reproductor precompiladas. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/D | Ya no proporcionamos asignaciones de reproductor precompiladas. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/D | La finalización del contenido solo admite un marcador de progreso del 100%. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/D | La finalización del contenido solo admite un marcador de progreso del 100%. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | SDK Key: playerName;<br> API Key: media.playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/A | Media Analytics tiene establecido 10 segundos para el contenido y 1 segundo para los anuncios. No hay más opciones disponibles. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/A | Media Analytics siempre realiza un seguimiento de los marcadores de progreso en el 10 %, 25 %, 50 %, 75 % y 95 %. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/A | Media Analytics siempre realiza un seguimiento de los marcadores de progreso en el 10 %, 25 %, 50 %, 75 % y 95 %. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/A | El seguimiento automático ya no está disponible. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/A | El seguimiento automático ya no está disponible. |

### Variables de seguimiento de publicidades

| Milestone | Sintaxis de Milestone | Media Analytics | Sintaxis de Media Analytics |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/A | Media Analytics tiene establecido 10 segundos para el contenido y 1 segundo para los anuncios. No hay más opciones disponibles. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/D | Los marcadores de progreso no se proporcionan de forma predeterminada para las publicidades. Utilice métricas calculadas para crear marcadores de progreso de anuncios. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/D | Media Analytics se establece en 1 segundo para las publicidades. No hay más opciones disponibles. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/A | El seguimiento automático ya no está disponible. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/A | El seguimiento automático ya no está disponible. |

### Métodos de módulo multimedia

| Milestone | Sintaxis de Milestone | Media Analytics | Sintaxis de Media Analytics |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | trackSessionStart | `trackSessionStart(` <br> `  mediaObject,` <br> `  contextData)` |
| mediaName - (Required) <br> The name of the video as you want it to appear in video reports. | `mediaName` | name | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaLength - (Required) <br> The length of the video in seconds. | `mediaLength` | length | `createMediaObject(` <br> `  name,` <br> `  mediaId,` <br> `  length,` <br> `  streamType)` |
| mediaPlayerName - (Required) <br> The name of the media player used to view the video, as you want it to appear in video reports. | `mediaPlayerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | trackEvent | `mediaHeartbeat.trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdBreakStart, ` <br> `  adBreakObject);` <br> `...` <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `    Event.` <br> `    AdStart, ` <br> `  adObject, ` <br> `  adCustomMetadata);` |
| name - (Required) <br> The name or ID of the ad. | `name` | name | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| length - (Required) <br> The length of the ad. | `length` | length | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| playerName - (Required) <br> The name of the media player used to view the ad. | `playerName` | playerName | `MediaHeartbeatConfig.` <br> `  playerName` |
| parentName <br> The name or ID of the primary content where the ad is embedded. | `parentName` | N/D | Heredado automáticamente |
| parentPod <br> The position in the primary content the ad was played. | `parentPod` | position | `createAdBreakObject(` <br> `  name, ` <br> `  position, ` <br> `  startTime)` |
| parentPodPosition <br> The position within the pod where the ad is played. | `parentPodPosition` | position | `createAdObject(` <br> `  name, ` <br> `  adId, ` <br> `  position, ` <br> `  length)` |
| CPM <br> The CPM or encrypted CPM (prefixed with a &quot;~&quot;) that applies to this playback. | `CPM` | N/A | No disponible de forma predeterminada en Media Analytics. |
| Media.click | `s.Media.click(` <br> `  name,` <br> `  offset)` | N/D | Utilice una llamada de análisis de vínculos personalizada para rastrear clics. |
| Media.close | `s.Media.close(` <br> `  mediaName)` | trackSessionEnd | `trackSessionEnd()` |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | trackComplete | `trackComplete()` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | trackPlay | `trackPlay()` |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | trackPause<br> o <br>trackEvent | `trackPause()` <br> o `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  SeekStart)` <br> o <br> `trackEvent(` <br> `  MediaHeartbeat.` <br> `  Event.` <br> `  BufferStart);` |
| Media.monitor | `s.Media.monitor(s, media)` | Utilice metadatos personalizados o estándar para establecer variables adicionales. | `var customVideoMetadata = ` <br> `{` <br> `  isUserLoggedIn: ` <br> `    "false",` <br> `  tvStation: ` <br> `    "Sample TV station",` <br> `  programmer: ` <br> `    "Sample programmer"` <br> `};` <br> `...` <br> `var standardVideoMetadata ` <br> `  = {};` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   EPISODE] = ` <br> `  "Sample Episode";` <br> `standardVideoMetadata` <br> `  [MediaHeartbeat.` <br> `   VideoMetadataKeys.` <br> `   SHOW] = "Sample Show";` <br> `...` <br> `mediaObject.setValue(` <br> `  MediaHeartbeat.` <br> `  MediaObjectKey.` <br> `  StandardVideoMetadata, ` <br> `  standardVideoMetadata);` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | N/D | La frecuencia de llamada de seguimiento se configura automáticamente. |

