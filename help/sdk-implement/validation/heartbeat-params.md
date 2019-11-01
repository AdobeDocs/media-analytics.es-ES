---
title: Descripciones de parámetros de Heartbeat
description: Una lista de los parámetros de latidos que Adobe recopila y procesa en el servidor de Media Analytics (latidos).
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Descripciones de parámetros de Media Analytics (latidos){#heartbeat-parameter-descriptions}

Lista de parámetros de Media Analytics que Adobe recopila y procesa en el servidor de Media Analytics (latidos):

## Todos los eventos

| Nombre | Fuente de datos |  Descripción  |
| ---  | --- | --- |
| s:event:type | Media SDK | (Required)<br/><br/>The type of the event being tracked. Tipos de eventos: <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=chapter_start </li> <li> s:event:type=chapter_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=resume </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:event:prev_ts | Media SDK | (Required)<br/><br/>The timestamp of the last event of the same type in this session. El valor es -1. |
| l:event:ts | Media SDK | (Required)<br/><br/>The timestamp of the event. |
| l:event:duration | Media SDK | (Required)<br/><br/>This value is set internally (in milliseconds) by the Media SDK, not by the player. Se utiliza para calcular las métricas de tiempo invertido en el servidor. Por ejemplo: a.media.totalTimePlayed se calcula como una suma de la duración de todos los latidos de reproducción (type=play) que se generan. <br/>** Nota: Este parámetro se establece en 0 para ciertos eventos porque son "eventos de cambio de estado" (por ejemplo, type=complete, type=chapter_complete o type=bitrate_change). |
| l:event:playhead | VideoInfo | (Required)<br/><br/>The playhead was inside the currently active asset (main or ad), when the event was recorded. |
| s:event:sid | Media SDK | (Required)<br/><br/>The session ID (a randomly generated string). Todos los eventos de una sesión determinada (vídeo + anuncios) deben ser los mismos. |
| l:asset:duration / l:asset:length <br/>(Se cambió el nombre de la duración) | VideoInfo | (Required)<br/><br/>The video asset length of the main asset. |
| s:asset:publisher | MediaHeartbeatConfig | (Required)<br/><br/>The publisher of the asset. |
| s:asset:video_id | VideoInfo | (Required)<br/><br/>An ID uniquely identifying the video in the publisher's catalog. |
| s:asset:type | Media SDK | (Required)<br/><br/>The asset type (main or ad). |
| s:stream:type | VideoInfo | (Requerido)<br/><br/>El tipo de flujo. Puede ser uno de los siguientes: <ul> <li> live </li> <li> vod </li> <li> lineal </li> </ul> |
| s:user:id | Objeto Configuration para dispositivos móviles, medición de aplicaciones VisitorID | (Optional)<br/><br/>User's specifically set Visitor ID. |
| s:user:aid | Org. de Experience Cloud | (Optional)<br/><br/>The user's Analytics Visitor ID value. |
| s:user:mid | Org. de Experience Cloud | (Required)<br/><br/>The user's Experience cloud visitor ID value. |
| s:cuser:customer_user_ids_x | MediaHeartbeatConfig | (Optional)<br/><br/>All customer user IDs set on Audience Manager. |
| l:aam:loc_hint | MediaHeartbeatConfig | (Required)<br/><br/>AAM data sent on each payload after aa_start |
| s:aam:blob | MediaHeartbeatConfig | (Required)<br/><br/>AAM data sent on each payload after aa_start |
| s:sc:rsid | ID (o identificadores) del grupo de informes | (Requerido)RSID de<br/><br/>Adobe Analytics donde se deben enviar los informes. |
| s:sc:tracking_server | MediaHeartbeatConfig | (Requerido) Servidor de seguimiento de<br/><br/>Adobe Analytics. |
| h:sc:ssl | MediaHeartbeatConfig | (Required)<br/><br/>Whether the traffic is over HTTPS (if set to 1) or over HTTP (is set to 0). |
| s:sp:ovp | MediaHeartbeatConfig | (Optional)<br/><br/>Set to "primetime" for Primetime players, or the actual OVP for other players. |
| s:sp:sdk | MediaHeartbeatConfig | (Required)<br/><br/>The OVP version string. |
| s:sp:player_name | VideoInfo | (Required)<br/><br/>Video player name (the actual player software, used to identify the player). |
| s:sp:channel | MediaHeartbeatConfig | (Optional)<br/><br/>The channel where the user is watching the content. En aplicaciones móviles, el nombre de la aplicación. En sitios web, el nombre del dominio. |
| s:sp:hb_version | Media SDK | (Requerido)<br/><br/>El número de versión de la biblioteca del SDK de medios que emite la llamada. |
| l:stream:bitrate | QoSInfo | (Required)<br/><br/>The current value of the stream bitrate (in bps). |

## Eventos de error

| Nombre | Fuente de datos | Descripción   |
| ---  | --- | --- |
| s:event:source | Media SDK | (Required)<br/><br/>The source of the error, either player-internal, or the application-level. |
| s:event:id | Media SDK | (Required)<br/><br/>Error ID, uniquely identifies the error. |

## Eventos de anuncio

| Nombre | Fuente de datos | Descripción   |
| ---  | --- | --- |
| s:asset:ad_id | AdInfo | (Requerido)<br/><br/>El nombre de la publicidad. |
| s:asset:ad_sid | Media SDK | (Required)<br/><br/>A unique identifier generated by the Media SDK, appended to all ad-related pings. |
| s:asset:pod_id | Media SDK | (Required)<br/><br/>Pod ID inside the video. Este valor se calcula automáticamente en función de la siguiente fórmula: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s:asset:pod_position | AdBreakInfo | (Required)<br/><br/>Index of the ad inside the pod (the first ad has index 0, the second ad has index 1, etc.). |
| s:asset:resolver | AdBreakInfo | (Requerido)<br/><br/>La resolución de publicidad. |
| s:meta:custom_ad_metadata.x | MediaHeartbeat | (Optional)<br/><br/>The custom ad metadata. |

## Eventos de capítulo

| Nombre | Fuente de datos | Descripción   |
| ---  | --- | --- |
| s:stream:chapter_sid | Media SDK | (Required)<br/><br/>The unique identifier associated to the playback instance of the chapter.  <br/> **Nota:** Un capítulo se puede reproducir varias veces debido a las operaciones seek-back realizadas por el usuario. |
| s:stream:chapter_name | ChapterInfo | (Optional)<br/><br/>The chapter's friendly (i.e., human readable) name. |
| s:stream:chapter_id | Media SDK | (Required)<br/><br/>The unique ID of the chapter. Este valor se calcula automáticamente en función de la siguiente fórmula: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:stream:chapter_pos | ChapterInfo | (Required)<br/><br/>The chapter's index in the list of chapters (starting with 1). |
| l:stream:chapter_offset | ChapterInfo | (Required)<br/><br/>The chapter's offset (expressed in seconds) inside the main content, excluding ads. |
| l:stream:chapter_length | ChapterInfo | (Required)<br/><br/>The chapter's duration (expressed in seconds). |
| s:meta:custom_chapter_metadata.x | ChapterInfo | (Opcional) Metadatos de capítulo<br/><br/>personalizados. |

## Evento Fin de la sesión

| Nombre | Fuente de datos | Descripción   |
| ---  | --- | --- |
| s:event:type=end | Media SDK | (Requerido)<br/><br/> El `end``close` |

