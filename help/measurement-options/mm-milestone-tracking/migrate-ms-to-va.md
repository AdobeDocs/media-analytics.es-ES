---
title: Migración de Milestone a Media Analytics
description: null
uuid: fdc96146-af63-48ce-b938-c0ca70729277
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Migración de Milestone a Media Analytics {#migrating-from-milestone-to-media-analytics}

## Información general {#overview}

Los conceptos principales de la medición de vídeo son los mismos para Milestone y Media Analytics, que lleva eventos de reproductor de vídeo y los asigna a métodos de análisis, al tiempo que toma metadatos y valores del reproductor y los asigna a variables de análisis. La solución de Media Analytics se desarrolló a partir de Milestone, por lo que muchos de los métodos y métricas son los mismos; sin embargo, el enfoque de configuración y el código han cambiado significativamente. Debería ser posible actualizar el código de evento del reproductor para que indique los nuevos métodos de Media Analytics. Consulte [Información general de SDK](/help/sdk-implement/setup/setup-overview.md) e [Información general del seguimiento](/help/sdk-implement/track-av-playback/track-core-overview.md) para obtener más información sobre la implementación de Media Analytics.

En las tablas siguientes se proporcionan las correspondencias entre la solución Milestone y la solución Media Analytics.

## Guía de migración {#migration-guide}

### Referencia de variable

| Métrica de Milestone | Tipo de variable | Métrica de Media Analytics |
| --- | --- | --- |
| Contenido | <br/><br/>Caducidad predeterminada de la eVar: Visita | Contenido |
| Tipo de contenido | <br/><br/>Caducidad predeterminada de la eVar: Vista de página | Tipo de contenido |
| Tiempo invertido en contenido | Tipo de evento<br/><br/>: Contador | Tiempo invertido en contenido |
| Inicios de vídeo | Tipo de evento<br/><br/>: Contador | Inicios de vídeo |
| Vídeos completados | Tipo de evento<br/><br/>: Contador | Contenido finalizado |

### Variables de módulo multimedia

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintaxis de Milestone
</th>
<th>Media Analytics
</th>
<th>Sintaxis de Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.trackUsingContextData
</td>
<td>
<pre>
s.Media.trackUsingContextData
  = true;
</pre>
</td>
<td>N/D
</td>
<td>Todos los datos de Media Analytics solo se envían mediante datos de contexto.
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.contextDataMapping = {
  "a.media.name":"eVar2,prop2",
  "a.media.segment":"eVar3",
  "a.contentType":"eVar1",
  "a.media.timePlayed":"event3",
  "a.media.view":"event1",
  "a.media.segmentView":"event2",
  "a.media.complete":"event7",
  "a.media.milestones": {
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
</pre>
</td>
<td>N/D
</td>
<td>Los datos de contexto de Media Analytics se rellenan automáticamente en las variables reservadas. Ya no es necesario asignar eVars, props y eventos en el código de implementación. Los clientes pueden asignar datos de contexto a variables mediante el uso de reglas de procesamiento.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s.Media.trackVars = 
  "events,
  prop2,
  eVar1,
  eVar2,
  eVar3";
</pre>
</td>
<td>N/D
</td>
<td>Ya no es necesario puesto que se realiza mediante variables reservadas y reglas de procesamiento.
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents = 
  "event1,
  event2,
  event3,
  event4,
  event5,
  event6,
  event7"
</pre>
</td>
<td>N/D
</td>
<td>Ya no es necesario puesto que se realiza mediante variables reservadas y reglas de procesamiento.
</td>
</tr>
</tbody>
</table>

### Variables opcionales

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintaxis de Milestone
</th>
<th>Media Analytics
</th>
<th>Sintaxis de Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.autoTrack
</td>
<td>
<pre>
s.Media.autoTrack
  = true;
</pre>
</td>
<td>N/D
</td>
<td>Ya no proporcionamos asignaciones de reproductor precompiladas.
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.
  autoTrackNetStreams
  = true
</pre>
</td>
<td>N/D
</td>
<td>Ya no proporcionamos asignaciones de reproductor precompiladas.
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.
  completeByCloseOffset
  = true
</pre>
</td>
<td>N/D
</td>
<td>La finalización del contenido solo admite un marcador de progreso del 100%.
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  completeCloseOffsetThreshold
  = 1
</pre>
</td>
<td>N/D
</td>
<td>La finalización del contenido solo admite un marcador de progreso del 100%.
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName
  = "Nombre de reproductor personalizado"
</pre>
</td>
<td>
Clave de SDK: playerName; Clave de API: media.playerName
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</p>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.
  trackSeconds
  = 15
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics tiene establecido 10 segundos para el contenido y 1 segundo para los anuncios. No hay más opciones disponibles.
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.
  trackMilestones
  = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics siempre realiza un seguimiento de los marcadores de progreso en el 10 %, 25 %, 50 %, 75 % y 95 %.
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  trackOffsetMilestones
  = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics siempre realiza un seguimiento de los marcadores de progreso en el 10 %, 25 %, 50 %, 75 % y 95 %.
</td>
</tr>
<tr>
<td>
Media.segmentByMilestones
</td>
<td>
<pre>
s.Media.segmentByMilestones
  = true;
</pre>
</td>
<td>N/D
</td>
<td>El seguimiento automático ya no está disponible
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  segmentByOffsetMilestones
  = true;
</pre>
</td>
<td>N/D
</td>
<td>El seguimiento automático ya no está disponible
</td>
</tr>
</tbody>
</table>

### Variables de seguimiento de publicidades

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintaxis de Milestone
</th>
<th>Media Analytics
</th>
<th>Sintaxis de Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.adTrackSeconds
</td>
<td>
<pre>
s.Media.
  adTrackSeconds
  = 15
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics tiene establecido 10 segundos para el contenido y 1 segundo para los anuncios. No hay más opciones disponibles.
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.
  adTrackMilestones
  = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Los marcadores de progreso no se proporcionan de forma predeterminada para las publicidades. Utilice métricas calculadas para crear marcadores de progreso de anuncios.
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adTrackOffsetMilestones
  = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics se establece en 1 segundo para las publicidades. No hay más opciones disponibles.
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByMilestones
  = true;
</pre>
</td>
<td>N/D
</td>
<td>El seguimiento automático ya no está disponible
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  adSegmentByOffsetMilestones
  = true;
</pre>
</td>
<td>N/D
</td>
<td>El seguimiento automático ya no está disponible
</td>
</tr>
</tbody>
</table>

### Métodos de módulo multimedia

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintaxis de Milestone
</th>
<th>Media Analytics
</th>
<th>Sintaxis de Media Analytics
</th>
</tr>
</thead>
<tbody>
<tr>
<td>
Media.open
</td>
<td>
<pre>
s.Media.open(
  mediaName,
  mediaLength,
  mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
trackSessionStart(
  mediaObject, 
  contextData)
</pre>
</td>
</tr>
<tr>
<td>
mediaName- (Obligatorio) El nombre del vídeo tal como desea que aparezca en informes de vídeo.
</td>
<td>
<pre>
mediaName
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createMediaObject(
  name, 
  mediaId, 
  length, 
  streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaLength - (Obligatorio) La duración del vídeo
en segundos.
</td>
<td>
<pre>
mediaLength
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createMediaObject(
  name, 
  mediaId, 
  length, 
  streamType)
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName - (Obligatorio) El nombre del reproductor de contenidos que se utilizó para ver el vídeo, tal como desea que aparezca en los informes de vídeo.
</td>
<td>
<pre>
mediaPlayerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
Media.openAd
</td>
<td>
<pre>
s.Media.openAd(
  name,
  length,
  playerName,
  parentName,
  parentPod,
  parentPodPosition,
  CPM)
</pre>
</td>
<td>
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
mediaHeartbeat.trackEvent(
  MediaHeartbeat.
    Evento.
    AdBreakStart, 
  adBreakObject);
...
trackEvent(
  MediaHeartbeat.
    Evento.
    AdStart, 
  adObject, 
  adCustomMetadata);
</pre>
</td>
</tr>
<tr>
<td>
name - (Obligatorio) El nombre o ID del anuncio.
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
name
</pre>
</td>
<td>
<pre>
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
length
(Obligatorio) La duración del anuncio.
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
length
</pre>
</td>
<td>
<pre>
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
playerName - (Obligatorio) El nombre del reproductor de contenidos
que se utilizó para ver el anuncio.
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
playerName
</pre>
</td>
<td>
<pre>
MediaHeartbeatConfig.
  playerName
</pre>
</td>
</tr>
<tr>
<td>
parentName - El nombre o ID del contenido primario donde está incrustado el anuncio.
</td>
<td>
<pre>
parentName
</pre>
</td>
<td>N/D
</td>
<td>Heredado automáticamente
</td>
</tr>
<tr>
<td>
parentPod - La posición en el contenido primario donde se reprodujo el anuncio.
</td>
<td>
<pre>
parentPod
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdBreakObject(
  name, 
  position, 
  startTime)
</pre>
</td>
</tr>
<tr>
<td>
parentPodPosition - La posición dentro del pod donde se reproduce el anuncio.
</td>
<td>
<pre>
parentPodPosition
</pre>
</td>
<td>
<pre>
position
</pre>
</td>
<td>
<pre>
createAdObject(
  name, 
  adId, 
  position, 
  length)
</pre>
</td>
</tr>
<tr>
<td>
CPM
El CPM o CPM cifrado (con el prefijo “~”) que se aplica a esta reproducción.
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>N/D
</td>
<td>No disponible de forma predeterminada en Media Analytics
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(
  name,
  offset)
</pre>
</td>
<td>N/D
</td>
<td>Utilice una llamada de análisis de vínculo personalizado para realizar un seguimiento de los clics.
</td>
</tr>
<tr>
<td>
Media.close
</td>
<td>
<pre>
s.Media.close(
  mediaName)
</pre>
</td>
<td>
<pre>
trackSessionEnd
</pre>
</td>
<td>
<pre>
trackSessionEnd()
</pre>
</td>
</tr>
<tr>
<td>
Media.complete
</td>
<td>
<pre>
s.Media.complete(
  name,
  offset)
</pre>
</td>
<td>
<pre>
trackComplete
</pre>
</td>
<td>
<pre>
trackComplete()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.play
</pre>
</td>
<td>
<pre>
s.Media.play(
  name,
  offset,
  segmentNum,
  segment,
  segmentLength)
</pre>
</td>
<td>
<pre>
trackPlay
</pre>
</td>
<td>
<pre>
trackPlay()
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.stop
</pre>
</td>
<td>
<pre>
s.Media.stop(
  mediaName,
  mediaOffset)
</pre>
</td>
<td>
<pre>
trackPause
</pre> O bien 
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
trackPause()
</pre> 
O bien
<pre>
trackEvent(
  MediaHeartbeat.
  Evento.
  SeekStart)
</pre> O bien
<pre>
trackEvent(
  MediaHeartbeat.
  Evento.
  BufferStart);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.monitor
</pre>
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>Utilice metadatos personalizados o estándar para establecer variables adicionales.
</td>
<td>
<pre>
var customVideoMetadata = 
{
  isUserLoggedIn: 
    "false",
  tvStation: 
    "Sample TV station",
  programmer: 
    "Sample programmer"
};
...
var standardVideoMetadata 
  = {};
standardVideoMetadata
  [MediaHeartbeat.
   VideoMetadataKeys.
   EPISODE] = 
  "Sample Episode";
standardVideoMetadata
  [MediaHeartbeat.
   VideoMetadataKeys.
   SHOW] = "Sample Show";
...
mediaObject.setValue(
  MediaHeartbeat.
  MediaObjectKey.
  StandardVideoMetadata, 
  standardVideoMetadata);
</pre>
</td>
</tr>
<tr>
<td>
<pre>
Media.track
</pre>
</td>
<td>
<pre>
s.Media.track(
  mediaName)
</pre>
</td>
<td>N/D
</td>
<td>La frecuencia de llamada de seguimiento se configura automáticamente.
</td>
</tr>
</tbody>
</table>

