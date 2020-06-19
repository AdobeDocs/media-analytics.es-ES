---
title: Migración de Milestone a vínculo personalizado
description: null
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
translation-type: tm+mt
source-git-commit: ccdc3e170d125a76d798be7ce1fa5c12eef1f76a
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 100%

---


# Migración de Milestone a vínculo personalizado {#migrating-from-milestone-to-custom-link}

## Información general {#overview}

Los conceptos básicos de la medición de vídeo son los mismos para el seguimiento de Milestone y el vínculo personalizado, ya que recopilan los eventos del reproductor de vídeo y los asignan a los métodos de análisis, a la vez que recogen los metadatos y valores del reproductor para asignarlos a las variables de análisis. El enfoque del vínculo personalizado debe entenderse como una reducción y simplificación de la implementación y los datos recopilados. Con la solución de vínculo personalizado, no existen variables ni métodos predefinidos para la medición de vídeo, sino que se requiere una configuración totalmente personalizada. Debería ser posible actualizar el código de evento del reproductor para que apunte a las llamadas de seguimiento del vínculo personalizado en el caso de los eventos básicos del reproductor, como el inicio y la finalización. Consulte [Guía de implementación de vínculo personalizado](/help/measurement-options/cl-in-aa/cl-impl-guide.md) y [Seguimiento de vínculo manual mediante el código de vínculo personalizado](https://docs.adobe.com/content/help/es-ES/media-analytics/using/measurement-options/cl-in-aa/cl-impl-guide.html) para obtener más información.

En las tablas siguientes se proporcionan las correspondencias entre la solución Milestone y la solución de vínculo personalizado.

## Guía de migración {#migration-guide}

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
<td>Tiempo invertido en contenido</td>
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
<th>Sintaxis de
</th>
<th>Sintaxis de Sintaxis
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
  trackUsingContextData 
  = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events, 
contextData.video.name’; 
s.contextData[‘video.name']
  = mediaName;
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
  contextDataMapping = {
  "a.media.name":
    "eVar2,prop2",
  "a.media.segment":
    "eVar3",
  "a.contentType":
    "eVar1",
  "a.media.timePlayed":
    "event3",
  "a.media.view":
    "event1",
  "a.media.segmentView":
    "event2",
  "a.media.complete":
    "event7",
  "a.media.milestones":{
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
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
s.Media.trackVars
  = "events,
     prop2,
     eVar1,
     eVar2,
     eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar13,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents
  = "event1,
     event2,
     event3,
     event4,
     event5,
     event6,
     event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents
  = 'event2';
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
<th>Sintaxis de
</th>
<th>Sintaxis de Sintaxis
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
  trackUsingContextData 
  = true;
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events, 
contextData.video.name’; 
s.contextData[‘video.name']
  = mediaName;
</pre>
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
  "a.media.milestones":{
    25:"event4",
    50:"event5",
    75:"event6"
  }
};
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
s.Media.trackVars
  = "events,
     prop2,
     eVar1,
     eVar2,
     eVar3";
</pre>
</td>
<td>
linkTrackVars
</td>
<td>
<pre>
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar13,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
</pre>
</td>
</tr>
<tr>
<td>
Media.trackEvents
</td>
<td>
<pre>
s.Media.trackEvents
  = "event1,
     event2,
     event3,
     event4,
     event5,
     event6,
     event7"
</pre>
</td>
<td>
linkTrackEvents
</td>
<td>
<pre>
s.linkTrackEvents
  = 'event2';
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
<th>Sintaxis de
</th>
<th>Sintaxis de Sintaxis
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
  completeCloseOffsetThreshold
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
s.contextData['video.player']
  = ”CustomPlayer Name”;
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
s.Media.trackOffsetMilestones 
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
  segmentByOffsetMilestones
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
<th>Sintaxis de
</th>
<th>Sintaxis de Sintaxis
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
  adTrackOffsetMilestones 
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
  adSegmentByMilestones
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
  adSegmentByOffsetMilestones
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
<th>Sintaxis de
</th>
<th>Sintaxis de Sintaxis
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
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.video.name,
     contextData.video.view';
s.linkTrackEvents 
  = 'event2';
s.prop10 
  = mediaName;
s.eVar10 
  = mediaName;
s.eVar12 
  = "video";
s.eVar15 
  = mediaPlayerName;
s.events 
  = 'event2';
s.contextData['video.name'] 
  = mediaName;
s.contextData['video.view'] 
  = 'true';
s.tl(this,'o','Video Start');
</pre>
</td>
</tr>
<tr>
<td>mediaName</td>
<td><b>mediaName:</b> (requerido) nombre del vídeo tal como desea que aparezca en informes de vídeo.</td>
<td>Defina la eVar o la variable de datos de contexto en la llamada al vínculo.</td>
<td>
<pre>
s.prop10 = mediaName;
s.eVar10 = mediaName;
s.contextData['video.name']
  = mediaName;
</pre>
</td>
</tr>
<tr>
<td>
mediaLength
</td>
<td>
<b>mediaLength</b>: (requerido) duración del vídeo en
segundos.
</td>
<td>
Defina la eVar o la variable de datos de contexto en la llamada al vínculo.
</td>
<td>
<pre>
s.contextData['video.length']
  = ”90”;
</pre>
</td>
</tr>
<tr>
<td>
mediaPlayerName
</td>
<td>
<b>mediaPlayerName</b>: (Obligatorio) nombre del reproductor multimedia
que se utilizó para ver el vídeo, tal como desea que aparezca
en informes de vídeo.
</td>
<td>
Defina la eVar o la variable de datos de contexto en la llamada al vínculo.
</td>
<td>
<pre>
s.contextData['video.player']
  = ”CustomPlayer Name”;
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
<td><b>name:</b> (requerido) nombre o ID del anuncio.</td>
<td>N/D</td>
<td>No disponible</td>
</tr>
<tr>
<td>
length
</td>
<td>
<b>length:</b> (requerido) duración del anuncio.
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
<b>playerName</b>: (requerido) nombre del reproductor de contenidos que se utilizó
para ver el anuncio.
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
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.complete';
s.linkTrackEvents 
  = 'event3';
s.prop10 
  = mediaName;
s.eVar10 
  = mediaName;
s.eVar12 
  = "video";
s.eVar15 
  = mediaPlayerName;
s.events 
  = 'event3';
s.contextData['video.name']
 =  mediaName;
s.contextData['video.complete']
 = 'true';
s.tl(this,'o','Video Complete');
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
s.linkTrackVars
  = 'events,
     prop10,
     eVar10,
     eVar12,
     eVar15,
     contextData.
       video.name,
     contextData.
       video.view';
s.linkTrackEvents = 'event2';
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

