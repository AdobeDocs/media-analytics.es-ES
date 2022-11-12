---
title: Obtenga información acerca de la migración de Milestone a vínculo personalizado
description: Aprenda a cambiar variables de Milestone por métodos de vínculo personalizado, y métodos de módulo de Milestone por sintaxis de vínculo personalizado.
uuid: 1c8edde5-0ef1-4bc0-a62d-1747f4907f09
exl-id: 732079f4-3eb8-4b9a-892b-25a1c9332be4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 9ba64b68efec5dd8b52010ac1a13afd7703448d0
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 100%

---

# Migración de Milestone a vínculo personalizado{#migrating-from-milestone-to-custom-link}

## Información general {#overview}

Los conceptos básicos de la medición de vídeo son los mismos para el seguimiento de Milestone y el vínculo personalizado, ya que recopilan los eventos del reproductor de vídeo y los asignan a los métodos de análisis, a la vez que recogen los metadatos y valores del reproductor para asignarlos a las variables de análisis. El enfoque del vínculo personalizado debe entenderse como una reducción y simplificación de la implementación y los datos recopilados. Con la solución de vínculo personalizado, no existen variables ni métodos predefinidos para la medición de vídeo, sino que se requiere una configuración totalmente personalizada. Debería ser posible actualizar el código de evento del reproductor para que apunte a las llamadas de seguimiento del vínculo personalizado en el caso de los eventos básicos del reproductor, como el inicio y la finalización. Consulte la [Guía de implementación de vínculos personalizados](/help/legacy/measurement-options/cl-in-aa/cl-impl-guide.md) para obtener más información.

En las tablas siguientes se proporcionan las correspondencias entre la solución Milestone y la solución de vínculo personalizado.

## Guía de migración {#migration-guide}

### Referencia de variables de vídeo

| Métrica de Milestone | Tipo de variable | Vínculo personalizado |
| --- | --- | --- |
| Contenido | <br>Caducidad predeterminada de la eVar: Visita | Defina su propia eVar. |
| Tipo de contenido | <br>Caducidad predeterminada de la eVar: Vista de página | Defina su propia eVar. |
| Tiempo invertido en contenido | Tipo de evento: <br>Contador | Defina su propio evento. |
| Inicios de vídeo | Tipo de evento: <br>Contador | Defina su propio evento. |
| Vídeos completados | Tipo de evento: <br>Contador | Defina su propio evento. |

### Variables de módulo multimedia

| Milestone | Sintaxis de Milestone | Vínculo personalizado | Vínculo personalizado Sintaxis |
| --- | --- | --- | --- |
| Media.trackUsingContextData | `s.Media.trackUsingContextData` <br> `  = true;` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `  contextData.video.name’;` <br> `  s.contextData["video.name"]` <br> `  = mediaName;` |
| Media.contextDataMapping | `s.Media.contextDataMapping = {` <br> `  "a.media.name":"eVar2,prop2",` <br> `  "a.media.segment":"eVar3",` <br> `  "a.contentType":"eVar1",` <br> `  "a.media.timePlayed":"event3",` <br> `  "a.media.view":"event1",` <br> `  "a.media.segmentView":"event2",` <br> `  "a.media.complete":"event7",` <br> `  "a.media.milestones": {` <br> `    25:"event4",` <br> `    50:"event5",` <br> `    75:"event6"` <br> `  }` <br> `};` | N/D | Ahora, la asignación de datos de contexto a eVars, props y eventos se realiza mediante reglas de procesamiento. |
| Media.trackVars | `s.Media.trackVars =` <br> `  "events,` <br> `  prop2,` <br> `  eVar1,` <br> `  eVar2,` <br> `  eVar3";` | linkTrackVars | `s.linkTrackVars` <br> `  = 'events,` <br> `    prop10,` <br> `    eVar10,` <br> `    eVar12,` <br> `    eVar13,` <br> `    eVar15,` <br> `    contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> |
| Media.trackEvents | `s.Media.trackEvents =` <br> `  "event1,` <br> `  event2,` <br> `  event3,` <br> `  event4,` <br> `  event5,` <br> `  event6,` <br> `  event7"` | linkTrackEvents | `s.linkTrackEvents` <br> `  = 'event2';` |

### Variables opcionales

| Milestone | Sintaxis de Milestone | Vínculo personalizado | Vínculo personalizado Sintaxis |
| --- | --- | --- | --- |
| Media.autoTrack | `s.Media.autoTrack` <br> `  = true;` | N/D | No disponible. |
| Media.autoTrackNetStreams | `s.Media.` <br> `  autoTrackNetStreams` <br> `  = true` | N/D | No disponible. |
| Media.completeByCloseOffset | `s.Media.` <br> `  completeByCloseOffset` <br> `  = true` | N/D | No disponible. |
| Media.completeCloseOffsetThreshold | `s.Media.` <br> `  completeCloseOffsetThreshold` <br> `  = 1` | N/D | No disponible. |
| Media.playerName | `s.Media.playerName` <br> `  = "Custom Player Name"` | Defina la eVar o la variable de datos de contexto en la llamada al vínculo. | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.trackSeconds | `s.Media.` <br> `  trackSeconds` <br> `  = 15` | N/D | No disponible. |
| Media.trackMilestones | `s.Media.` <br> `  trackMilestones` <br> `  = "25,50,75";` | N/D | No disponible. |
| Media.trackOffsetMilestones | `s.Media.` <br> `  trackOffsetMilestones` <br> `  = "20,40,60";` | N/D | No disponible. |
| Media.segmentByMilestones | `s.Media.segmentByMilestones` <br> `  = true;` | N/D | No disponible. |
| Media.segmentByOffsetMilestones | `s.Media.` <br> `  segmentByOffsetMilestones` <br> `  = true;` | N/D | No disponible. |

### Variables de seguimiento de anuncios

| Milestone | Sintaxis de Milestone | Vínculo personalizado | Vínculo personalizado Sintaxis |
| --- | --- | --- | --- |
| Media.adTrackSeconds | `s.Media.` <br> `  adTrackSeconds` <br> `  = 15` | N/D | No disponible. |
| Media.adTrackMilestones | `s.Media.` <br> `  adTrackMilestones` <br> `  = "25,50,75";` | N/D | No disponible. |
| Media.adTrackOffsetMilestones | `s.Media.` <br> `  adTrackOffsetMilestones` <br> `  = "20,40,60";` | N/D | No disponible. |
| Media.adSegmentByMilestones | `s.Media.` <br> `  adSegmentByMilestones` <br> `  = true;` | N/D | No disponible. |
| Media.adSegmentByOffsetMilestones | `s.Media.` <br> `  adSegmentByOffsetMilestones` <br> `  = true;` | N/D | No disponible. |

### Métodos de módulo multimedia

| Milestone | Sintaxis de Milestone | Vínculo personalizado | Vínculo personalizado Sintaxis |
| --- | --- | --- | --- |
| Media.open | `s.Media.open(` <br> `  mediaName,` <br> `  mediaLength,` <br> `  mediaPlayerName)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.view';` <br> `s.linkTrackEvents ` <br> `  = 'event2';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event2';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.view']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Start');` |
| mediaName | `mediaName`: (requerido) nombre del vídeo tal como desea que aparezca en informes de vídeo. | Defina la eVar o la variable de datos de contexto en la llamada al vínculo. | `s.prop10 = mediaName;` <br> `s.eVar10 = mediaName;` <br> `s.contextData['video.name']` <br> `  = mediaName;` |
| mediaLength | `mediaLength`: (requerido) duración del vídeo en segundos. | Defina la eVar o la variable de datos de contexto en la llamada al vínculo. | `s.contextData['video.length']` <br> `  = "90";` |
| mediaPlayerName | `mediaPlayerName`: (Obligatorio) nombre del reproductor multimedia que se utilizó para ver el vídeo, tal como desea que aparezca en informes de vídeo. | Defina la eVar o la variable de datos de contexto en la llamada al vínculo. | `s.contextData['video.player']` <br> `  = "CustomPlayer Name";` |
| Media.openAd | `s.Media.openAd(` <br> `  name,` <br> `  length,` <br> `  playerName,` <br> `  parentName,` <br> `  parentPod,` <br> `  parentPodPosition,` <br> `  CPM)` | N/D | No disponible. |
| name | `name`: (requerido) nombre o ID del anuncio. | N/D | No disponible. |
| length | `length`: (requerido) duración del anuncio. | N/D | No disponible. |
| playerName | `playerName`: (requerido) nombre del reproductor de contenidos que se utilizó para ver el anuncio. | N/D | No disponible. |
| parentName | `parentName`: Nombre o ID del contenido primario donde está incrustado el anuncio. | N/D | No disponible. |
| parentPod | `parentPod`: Posición en el contenido primario en que se reprodujo el anuncio. | N/D | No disponible. |
| parentPodPosition | `parentPodPosition`: Posición dentro del pod donde se reproduce el anuncio. | N/D | No disponible. |
| CPM | `CPM`: CPM o CPM cifrado (con el prefijo “~”) que se aplica a esta reproducción. | N/D | No disponible. |
| Media.click | `s.Media.click(name, offset)` | `s.tl()` | Utilice una llamada de análisis de vínculo personalizado para hacer un seguimiento de los clics. |
| Media.close | `s.Media.close(mediaName)` | N/D | No disponible. |
| Media.complete | `s.Media.complete(` <br> `  name,` <br> `  offset)` | `s.tl()` | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.video.name,` <br> `     contextData.video.complete';` <br> `s.linkTrackEvents ` <br> `  = 'event3';` <br> `s.prop10` <br> `   = mediaName;` <br> `s.eVar10` <br> `  = mediaName;` <br> `s.eVar12` <br> `  = "video";` <br> `s.eVar15` <br> `  = mediaPlayerName;` <br> `s.events` <br> `  = 'event3';` <br> `s.contextData['video.name']` <br> `  = mediaName;` <br> `s.contextData['video.complete']` <br> `  = 'true';` <br> `s.tl(this,'o','Video Complete');` |
| Media.play | `s.Media.play(` <br> `  name,` <br> `  offset,` <br> `  segmentNum,` <br> `  segment, ` <br> `  segmentLength)` | N/D | No disponible. |
| Media.stop | `s.Media.stop(` <br> `  mediaName,` <br> `  mediaOffset)` | N/D | No disponible. |
| Media.monitor | `s.Media.monitor(s, media)` | Defina la eVar o la variable de datos de contexto en la llamada al vínculo. | `s.linkTrackVars` <br> `  = 'events,` <br> `     prop10,` <br> `     eVar10,` <br> `     eVar12,` <br> `     eVar15,` <br> `     contextData.` <br> `       video.name,` <br> `     contextData.` <br> `       video.view';` <br> `s.linkTrackEvents = 'event2';` |
| Media.track | `s.Media.track(` <br> `  mediaName)` | N/D | No disponible. |
