---
seo-title: Migración de Milestone a vínculo personalizado
title: Migración de Milestone a vínculo personalizado
uuid: 1 c 8 edde 5-0 ef 1-4 bc 0-a 62 d -1747 f 4907 f 09
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Migración de Milestone a vínculo personalizado{#migrating-from-milestone-to-custom-link}

## Información general {#section_xlc_fc2_dfb}

Los conceptos básicos de la medición de vídeo son los mismos para el seguimiento de Milestone y el vínculo personalizado, ya que recopilan los eventos del reproductor de vídeo y los asignan a los métodos de análisis, a la vez que recogen los metadatos y valores del reproductor para asignarlos a las variables de análisis. El enfoque del vínculo personalizado debe entenderse como una reducción y simplificación de la implementación y los datos recopilados. Con la solución de vínculo personalizado, no existen variables ni métodos predefinidos para la medición de vídeo, sino que se requiere una configuración totalmente personalizada. Debería ser posible actualizar el código de evento del reproductor para que apunte a las llamadas de seguimiento del vínculo personalizado en el caso de los eventos básicos del reproductor, como el inicio y la finalización. Consulte [Guía de implementación de vínculo personalizado](/help/measurement-options/cl-in-aa/cl-impl-guide.md) y [Seguimiento de vínculo manual mediante el código de vínculo personalizado](https://marketing.adobe.com/resources/help/en_US/sc/implement/link_manual.html) para obtener más información.

En las tablas siguientes se proporcionan las correspondencias entre la solución Milestone y la solución de vínculo personalizado.

## Guía de migración {#section_btt_fc2_dfb}

### Referencia de variables de vídeo

<table>
<thead>
<tr>
<th><strong>Métrica de Milestone</strong></th>
<th><strong>Tipo de variable</strong></th>
<th><strong>Vínculo personalizado</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>Contenido</td>
<td>
<p>eVar</p>
<p>Caducidad predeterminada: visita</p>
</td>
<td>Defina su propia eVar.</td>
</tr>
<tr>
<td>Tipo de contenido</td>
<td>
<p>eVar</p>
<p>Caducidad predeterminada: vista de página</p>
</td>
<td>Defina su propia eVar.</td>
</tr>
<tr>
<td>tiempo invertido en contenido</td>
<td>
<p>Evento</p>
<p>Tipo: contador</p>
</td>
<td>Defina su propio evento.</td>
</tr>
<tr>
<td>Inicios de vídeo</td>
<td>
<p>Evento</p>
<p>Tipo: contador</p>
</td>
<td>Defina su propio evento.</td>
</tr>
<tr>
<td>Vídeos completados</td>
<td>
<p>Evento</p>
<p>Tipo: contador</p>
</td>
<td>Defina su propio evento.</td>
</tr>
</tbody>
</table>

### Variables de módulo multimedia

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintaxis de Milestone
</th>
<th>Vínculo personalizado
</th>
<th>Sintaxis de vínculo personalizado
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
s.Media.
  Trackusingcontextdata 
 = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events, 
contextdata. video. name '; 
s. contextdata [' video. name ']
 = medianame;
</pre>
</td>
</tr>
<tr>
<td>
Media.contextDataMapping
</td>
<td>
<pre>
s.Media.
  Contextdatamapping = {"a. media. name":
 " Evar 2, prop 2 ","
 a. media. segment ":
 " Evar 3 ","
 a. contenttype ":
 " Evar 1 ","
 a. media. timeplayed ":
 " event 3 ","
 a. media. view ":
 " event 1 ","
 a. media. segmentview ":
 " event 2 ","
 a. media. complete ":
 " event 7 ","
 a. media. milestones ": {25: " event 4 ",
 50: " event 5 ",
 75: " event 6 "}};
</pre>
</td>
<td>N/D
</td>
<td>Ahora, la asignación de datos de contexto a eVars, props y eventos se realiza mediante reglas de procesamiento.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s. Media. trackvars
 = "events,
 prop 2,
 evar 1,
 evar 2,
 evar 3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 13,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s. Media. trackevents
 = "event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s. linktrackevents
 =' event 2 ';
</pre>
</td>
</tr>
</tbody>
</table>

<table>
<thead>
<tr>
<th>Milestone
</th>
<th>Sintaxis de Milestone
</th>
<th>Vínculo personalizado
</th>
<th>Sintaxis de vínculo personalizado
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
s.Media.
  Trackusingcontextdata 
 = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events, 
contextdata. video. name '; 
s. contextdata [' video. name ']
 = medianame;
</pre>
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
<td>Ahora, la asignación de datos de contexto a eVars, props y eventos se realiza mediante reglas de procesamiento.
</td>
</tr>
<tr>
<td>
Media.trackVars
</td>
<td>
<pre>
s. Media. trackvars
 = "events,
 prop 2,
 evar 1,
 evar 2,
 evar 3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 13,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s. Media. trackevents
 = "event 1,
 event 2,
 event 3,
 event 4,
 event 5,
 event 6,
 event 7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s. linktrackevents
 =' event 2 ';
</pre>
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
<th>Vínculo personalizado
</th>
<th>Sintaxis de vínculo personalizado
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
<td>No disponible
</td>
</tr>
<tr>
<td>
Media.autoTrackNetStreams
</td>
<td>
<pre>
s.Media.autoTrackNetStreams = true
</pre>
</td>
<td>N/D
</td>
<td>No disponible
</td>
</tr>
<tr>
<td>
Media.completeByCloseOffset
</td>
<td>
<pre>
s.Media.completeByCloseOffset = true
</pre>
</td>
<td>N/D
</td>
<td>No disponible
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
<td>No disponible
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
Defina la eVar o la variable de datos de contexto en la llamada al vínculo.
</td>
<td>
<pre>
s. contextdata [' video. player ']
 =» Nombre de customplayer»;
</pre>
</td>
</tr>
<tr>
<td>
Media.trackSeconds
</td>
<td>
<pre>
s.Media.trackSeconds = 15
</pre>
</td>
<td>N/D
</td>
<td>No disponible
</td>
</tr>
<tr>
<td>
Media.trackMilestones
</td>
<td>
<pre>
s.Media.trackMilestones = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>No disponible
</td>
</tr>
<tr>
<td>
Media.trackOffsetMilestones
</td>
<td>
<pre>
s.Media.trackOffsetMilestones = "20,40,60";
</pre>
</td>
<td>N/D
</td>
<td>No disponible
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
<td>No disponible
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
<td>No disponible
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
<th>Vínculo personalizado
</th>
<th>Sintaxis de vínculo personalizado
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
s.Media.adTrackSeconds = 15 
</pre>
</td>
<td>N/D
</td>
<td>No disponible
</td>
</tr>
<tr>
<td>
Media.adTrackMilestones
</td>
<td>
<pre>
s.Media.adTrackMilestones = "25,50,75";
</pre>
</td>
<td>N/D
</td>
<td>No disponible
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
<td>No disponible
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
<td>No disponible
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
<td>No disponible
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
<th>Vínculo personalizado
</th>
<th>Sintaxis de vínculo personalizado
</th>
</tr>
</thead>
<tbody>
<tr>
<td>Media.open</td>
<td>
<pre>
s.Media.open(mediaName,mediaLength,mediaPlayerName)
</pre>
</td>
<td>s.tl()</td>
<td>
<pre>
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata. video. name,
 contextdata. video. view ';
s. linktrackevents 
 =' event 2 ';
s. prop 10 
 = Medianame;
s. evar 10 
 = Medianame;
s. evar 12 
 = "video";
s. evar 15 
 = Mediaplayername;
s. events 
 =' event 2 ';
s. contextdata [' video. name '] 
 = Medianame;
s. contextdata [' video. view '] 
 =' true ';
s. tl (this,' o ',' Video Start ');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b>Medianame:</b> (requerido) El nombre del vídeo como desee que aparezca en los informes de vídeo.</td>
<td>Defina la eVar o la variable de datos de contexto en la llamada al vínculo.</td>
<td>
<pre>
s. prop 10 = medianame;
s. evar 10 = medianame;
s. contextdata [' video. name ']
 = medianame;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b>Medialength:</b> (Requerido) Duración del video en
segundos.
</td>
<td>
Defina la eVar o la variable de datos de contexto en la llamada al vínculo.
</td>
<td>
<pre>
s. contextdata [' video. length ']
 =» 90»;
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b>Mediaplayername:</b> (requerido) El nombre del reproductor
de medios utilizado para ver el video, como desee que aparezca en los informes de video.
</td>
<td>
Defina la eVar o la variable de datos de contexto en la llamada al vínculo.
</td>
<td>
<pre>
s. contextdata [' video. player ']
 =» Nombre de customplayer»;
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
<td>N/D
</td>
<td>No disponible</td>
</tr>
<tr>
<td>name</td>
<td><b>name:</b> (requerido) Nombre o ID del anuncio.</td>
<td>N/D</td>
<td>No disponible</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>length:</b> (requerido) Duración de la publicidad.
</td>
<td>N/D
</td>
<td>No disponible
</td>
</tr>
<tr>
<td>
playerName
</td>
<td>
<b>Playername:</b> (requerido) Nombre del reproductor de medios utilizado
para ver la publicidad.
</td>
<td>N/D
</td>
<td>No disponible
</td>
</tr>
<tr>
<td>
parentName
</td>
<td>
<b>parentName</b>: nombre o ID del contenido primario donde está incrustado el anuncio.
</td>
<td>N/D
</td>
<td>No disponible
</td>
</tr>
<tr>
<td>
parentPod
</td>
<td>
<b>parentPod</b>: posición en el contenido primario en que se reprodujo el anuncio.
</td>
<td>N/D
</td>
<td>No disponible
</td>
</tr>
<tr>
<td>
parentPodPosition
</td>
<td>
<b>parentPodPosition</b>: posición dentro del pod donde se reproduce el anuncio.
</td>
<td>N/D
</td>
<td>No disponible
</td>
</tr>
<tr>
<td>
CPM
</td>
<td>
<b>CPM</b>: CPM o CPM cifrado (con el prefijo “~”) que se aplica a esta reproducción.
</td>
<td>N/D
</td>
<td>No disponible
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
<td>
<pre>
s.tl()
</pre>
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
<td>N/D
</td>
<td>No disponible
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
s.tl()
</td>
<td>
<pre>
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. complete ';
s. linktrackevents 
 =' event 3 ';
s. prop 10 
 = Medianame;
s. evar 10 
 = Medianame;
s. evar 12 
 = "video";
s. evar 15 
 = Mediaplayername;
s. events 
 =' event 3 ';
s. contextdata [' video. name ']
 = medianame;
s. contextdata [' video. complete ']
 =' true ';
s. tl (this,' o ',' Video Complete ');
</pre>
</td>
</tr>
<tr>
<td>
Media.play
</td>
<td>
<pre>
s.Media.play(name,offset,segmentNum,segment,segmentLength)
</pre>
</td>
<td>N/D
</td>
<td>No disponible
</td>
</tr>
<tr>
<td>
Media.stop
</td>
<td>
<pre>
s.Media.stop(mediaName,mediaOffset)
</pre>
</td>
<td>N/D 
</td>
<td>No disponible
</td>
</tr>
<tr>
<td>
Media.monitor
</td>
<td>
<pre>
s.Media.monitor(s, media)
</pre>
</td>
<td>
Defina la eVar o la variable de datos de contexto en la llamada al vínculo.
</td>
<td>
<pre>
s. linktrackvars
 =' events,
 prop 10,
 evar 10,
 evar 12,
 evar 15,
 contextdata.
 video. name,
 contextdata.
 video. view ';
s. linktrackevents =' event 2 ';
</pre>
</td>
</tr>
<tr>
<td>
Media.track
</td>
<td>
<pre>
s.Media.track(mediaName)
</pre>
</td>
<td>N/D
</td>
<td>No disponible
</td>
</tr>
</tbody>
</table>

