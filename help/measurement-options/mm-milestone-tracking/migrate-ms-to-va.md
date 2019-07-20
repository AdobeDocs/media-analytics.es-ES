---
seo-title: Migración de Milestone a Media Analytics
title: Migración de Milestone a Media Analytics
uuid: fdc 96146-af 63-48 ce-b 938-c 0 ca 70729277
translation-type: tm+mt
source-git-commit: 27740fc1753e8ac9cf5a4b240a56b1c2dd567010

---


# Migración de Milestone a Media Analytics {#migrating-from-milestone-to-media-analytics}

## Información general {#section_ihl_nbz_cfb}

Los conceptos básicos de la medición de vídeo son los mismos para Milestone y Media Analytics, ya que recopilan los eventos del reproductor de vídeo y los asignan a los métodos de análisis, a la vez que recogen los metadatos y valores del reproductor para asignarlos a las variables de análisis. La solución Media Analytics se desarrolló a partir de Milestone, por lo que muchos de los métodos y métricas son comunes. Sin embargo, el enfoque de la configuración y el código han cambiado considerablemente. Debería ser posible actualizar el código de evento del reproductor para que apunte a los nuevos métodos de Media Analytics. See [SDK Overview](../../sdk-implement/setup/setup-overview.md) and [Tracking Overview](../../sdk-implement/track-av-playback/track-core-overview.md) for more details on implementing Media Analytics.

En las tablas siguientes se proporcionan las correspondencias entre la solución Milestone y la solución Media Analytics.

## Guía de migración {#section_iyb_pbz_cfb}

### Referencia de variables

| Métrica de Milestone | Tipo de variable | Métrica de Media Analytics |
| --- | --- | --- |
| Contenido | eVar<br/><br/>Default expiration: Visit | Contenido |
| Tipo de contenido | eVar<br/><br/> Default expiration: Page view | Tipo de contenido |
| tiempo invertido en contenido | Event<br/><br/> Type: Counter | tiempo invertido en contenido |
| Inicios de vídeo | Event<br/><br/> Type: Counter | Inicios de vídeo |
| Vídeos completados | Evento<br/><br/> Tipo: contador | Contenido finalizado |

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
s.Media.trackUsingContextData = true;
</pre>
</td>
<td>N/D
</td>
<td>Los datos de Media Analytics solo se envían mediante el uso de datos de contexto.
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s. Media. contextdatamapping = {"a. media. name": " Evar 2, prop 2 ","
 a. media. segment ": " Evar 3 ","
 a. contenttype ": " Evar 1 ","
 a. media. timeplayed ": " event 3 ","
 a. media. view ": " event 1 ","
 a. media. segmentview ": " event 2 ","
 a. media. complete ": " event 7 ","
 a. media. milestones ": {25: " event 4 ",
 50: " event 5 ",
 75: " event 6 "}};
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
s. Media. trackvars = 
 " events,
 prop 2,
 evar 1,
 evar 2,
 evar 3 ";
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
s. Media. trackevents = 
 " event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7 "
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
s.Media.autoTrack = true;
</pre>
</td>
<td>N/D
</td>
<td>Ya no proporcionamos asignaciones de reproductor predefinidas.
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.
  Autotracknetstreams
 = true
</pre>
</td>
<td>N/D
</td>
<td>Ya no proporcionamos asignaciones de reproductor predefinidas.
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.
  Completebycloseoffset
 = true
</pre>
</td>
<td>N/D
</td>
<td>El contenido finalizado solo admite un marcador de progreso del 100 %.
</td>
</tr>
<tr>
<td>
Media.completeCloseOffsetThreshold
</td>
<td>
<pre>
s.Media.
  Completecloseoffsetthreshold
 = 1
</pre>
</td>
<td>N/D
</td>
<td>El contenido finalizado solo admite un marcador de progreso del 100 %.
</td>
</tr>
<tr>
<td>
Media.playerName
</td>
<td>
<pre>
s.Media.playerName = "Nombre de reproductor personalizado"
</pre>
</td>
<td>
Clave del SDK: Playername; 
Clave de API: media. playername
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
  Trackseconds
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
  Trackmilestones
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
  Trackoffsetmilestones
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
s.Media.segmentByMilestones = true;
</pre>
</td>
<td>N/D
</td>
<td>El seguimiento automático ya no está disponible.
</td>
</tr>
<tr>
<td>
Media.segmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  Segmentbyoffsetmilestones
 = true;
</pre>
</td>
<td>N/D
</td>
<td>El seguimiento automático ya no está disponible.
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
  Adtrackseconds
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
  Adtrackmilestones
 = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>Los marcadores de progreso no se proporcionan de forma predeterminada para los anuncios. Utilice métricas calculadas para crear marcadores de progreso de anuncios.
</td>
</tr>
<tr>
<td>
Media.adTrackOffsetMilestones
</td>
<td>
<pre>
s.Media.
  Adtrackoffsetmilestones
 = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>Media Analytics tiene establecido 1 segundo para los anuncios. No hay más opciones disponibles.
</td>
</tr>
<tr>
<td>
Media.adSegmentByMilestones
</td>
<td>
<pre>
s.Media.
  Adsegmentbymilestones
 = true;
</pre>
</td>
<td>N/D
</td>
<td>El seguimiento automático ya no está disponible.
</td>
</tr>
<tr>
<td>
Media.adSegmentByOffsetMilestones
</td>
<td>
<pre>
s.Media.
  Adsegmentbyoffsetmilestones
 = true;
</pre>
</td>
<td>N/D
</td>
<td>El seguimiento automático ya no está disponible.
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
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>
<pre>
trackSessionStart
</pre>
</td>
<td>
<pre>
Tracksessionstart (mediaobject, 
 Contextdata)
</pre>
</td>
</tr>
<tr>
<td>
Medianame: (Requerido) El nombre del vídeo como
desea que aparezca en los informes de vídeo.
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
Createmediaobject (name, 
 Mediaid, 
 length, 
 Streamtype)
</pre>
</td>
</tr>
<tr>
<td>
Medialength - (Requerido) Duración del video
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
Createmediaobject (name, 
 Mediaid, 
 length, 
 Streamtype)
</pre>
</td>
</tr>
<tr>
<td>
Mediaplayername: (Requerido) el nombre del reproductor de medios utilizado para ver el vídeo, 
como desea que aparezca en los informes de video.
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
s.Media.openAd(name,length,playerName,parentName,parentPod,parentPodPosition,CPM)
</pre>
</td>
<td>
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
Mediaheartbeat. trackevent (mediaheartbeat.
 Evento.
    Adbreakstart, 
 Adbreakobject);
…
Trackevent (mediaheartbeat.
 Evento.
    Adstart, 
 Adobject, 
 Adcustommetadata);
</pre>
</td>
</tr>
<tr>
<td>
name: (Requerido) nombre o ID del anuncio.
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
Createadobject (name, 
 Adid, 
 position, 
 length)
</pre>
</td>
</tr>
<tr>
<td>
length
(Requerido) Duración de la publicidad.
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
Createadobject (name, 
 Adid, 
 position, 
 length)
</pre>
</td>
</tr>
<tr>
<td>
Playername: (Requerido) el nombre del reproductor de medios
utilizado para ver la publicidad.
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
Parentname: nombre o ID del contenido principal en el que está incrustado el anuncio.
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
Parentpod: posición en el contenido principal en el que se reprodujo el anuncio.
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
Createadbreakobject (name, 
 position, 
 Starttime)
</pre>
</td>
</tr>
<tr>
<td>
Parentpodposition: posición dentro de la secuencia en la que se reproduce el anuncio.
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
Createadobject (name, 
 Adid, 
 position, 
 length)
</pre>
</td>
</tr>
<tr>
<td>
CPM
El CPM o CPM cifrado (con el prefijo «~») que se aplica a esta reproducción.
</td>
<td>
<pre>
CPM
</pre>
</td>
<td>N/D
</td>
<td>No está disponible de forma predeterminada en Media Analytics
</td>
</tr>
<tr>
<td>
Media.click
</td>
<td>
<pre>
s.Media.click(name,offset)
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
s.Media.close(mediaName)
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
s.Media.complete(name,offset)
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
s.Media.play(name,offset,segmentNum,segment,segmentLength)
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
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>
<pre>
trackPause
</pre> o 
<pre>
trackEvent
</pre>
</td>
<td>
<pre>
trackPause()
</pre> 
o
<pre>
Trackevent (mediaheartbeat.
 Evento.
  SeekStart)
</pre> o
<pre>
Trackevent (mediaheartbeat.
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
var customvideometadata = 
{isuserloggedin: 
 " false ",
 tvstation: 
 " Estación de TV de muestra ",
 programador: 
 " Sample programmer "};
…
var standardvideometadata 
 = {};
Standardvideometadata
 [mediaheartbeat.
 VideoMetadataKeys.
   EPISODE] = 
 " Episode de muestra ";
Standardvideometadata
 [mediaheartbeat.
 VideoMetadataKeys.
   SHOW] = "Muestra de muestra";
…
Mediaobject. setvalue (mediaheartbeat.
 Mediaobjectkey.
 Standardvideometadata, 
 Standardvideometadata);
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
s.Media.track(mediaName)
</pre>
</td>
<td>N/D
</td>
<td>La frecuencia de la llamada de seguimiento se establece automáticamente.
</td>
</tr>
</tbody>
</table>

