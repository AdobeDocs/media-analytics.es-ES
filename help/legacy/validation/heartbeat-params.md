---
title: Descripciones del parámetro de latido
description: Explore los parámetros de latido que Adobe recopila y procesa en el servidor de latidos de Media Analytics.
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: Streaming Media, Variables
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/kBThvgKw7QOwvcWzdGwwipkudTGhhbLB0BRq-z3PPWQ
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
  - id: e992d880-33bc-4949-a648-aa7d410276cd
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 672
ht-degree: 99%

---

# Descripciones de parámetros de Media Analytics (latidos){#heartbeat-parameter-descriptions}

Lista de parámetros de Media Analytics que Adobe recopila y procesa en el servidor de Media Analytics (latidos):

## Todos los eventos

| Nombre | Fuente de datos |  Descripción  |
| ---  | --- | --- |
| `s:event:type` | Media SDK | (Obligatorio)<br/><br/>Tipo de evento que se rastrea. Tipos de eventos: <ul> <li> s:event:tipo=inicio </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | Media SDK | (Obligatorio)<br/><br/>Marca de fecha del último evento del mismo tipo en esta sesión. El valor es -1. |
| `l:event:ts` | Media SDK | (Obligatorio)<br/><br/>Marca de tiempo del evento. |
| `l:event:duration` | Media SDK | (Obligatorio)<br/><br/>Este valor se establece internamente (en milisegundos) por Media SDK, no por el reproductor. Se utiliza para calcular las métricas de tiempo invertido en el servidor. Por ejemplo, a.media.totalTimePlayed se calcula como una suma de la duración de todos los latidos de reproducción (type=play) que se generan. <br/>*Nota:* Este parámetro se establece en 0 para ciertos eventos porque son “eventos de cambio de estado” (por ejemplo, type=complete, type=chapter_complete o type=bitrate_change). |
| `l:event:playhead` | VideoInfo | (Obligatorio)<br/><br/>El cabezal de reproducción estaba dentro del recurso activo (principal o anuncio), cuando se registró el evento. |
| `s:event:sid` | Media SDK | (Obligatorio)<br/><br/>El ID de sesión (una cadena generada aleatoriamente). Todos los eventos de una sesión determinada (vídeo + anuncios) deben ser los mismos. |
| `l:asset:duration` / `l:asset:length` <br/> (Se cambió el nombre de la duración) | VideoInfo | (Obligatorio)<br/><br/>La duración del recurso de vídeo del recurso principal. |
| `s:asset:publisher` | MediaHeartbeatConfig | (Obligatorio)<br/><br/>El editor del recurso. |
| `s:asset:video_id` | VideoInfo | (Obligatorio)<br/><br/>ID que identifica de forma exclusiva el vídeo en el catálogo del editor. |
| `s:asset:type` | Media SDK | (Obligatorio)<br/><br/>El tipo de recurso (principal o anuncio). |
| `s:stream:type` | VideoInfo | (Obligatorio)<br/><br/>El tipo de flujo. Puede ser uno de los siguientes: <ul> <li> live </li> <li> vod </li> <li> lineal </li> </ul> |
| `s:user:id` | Objeto Configuration para dispositivos móviles, medición de aplicaciones VisitorID | (Obligatorio)<br/><br/>El usuario ha definido específicamente el ID de visitante. |
| `s:user:aid` | Org. de Experience Cloud | (Obligatorio)<br/><br/>El valor de ID de visitante de Analytics del usuario. |
| `s:user:mid` | Org. de Experience Cloud | (Obligatorio)<br/><br/>El valor de ID de visitante de Experience Cloud del usuario. |
| `s:cuser:customer_user_ids_x` | MediaHeartbeatConfig | (Obligatorio)<br/><br/>Todos los ID de usuario de cliente definidos en Audience Manager. |
| `l:aam:loc_hint` | MediaHeartbeatConfig | (Obligatorio)<br/><br/>Los datos de AAM enviados en cada carga útil después de aa_start. |
| `s:aam:blob` | MediaHeartbeatConfig | (Obligatorio)<br/><br/>Los datos de AAM enviados en cada carga útil después de aa_start. |
| `s:sc:rsid` | ID (o identificadores) del grupo de informes | (Obligatorio)<br/><br/>RSID de Adobe Analytics donde se deben enviar los informes. |
| `s:sc:tracking_server` | MediaHeartbeatConfig | (Obligatorio)<br/><br/>Servidor de seguimiento de Adobe Analytics. |
| `h:sc:ssl` | MediaHeartbeatConfig | (Obligatorio)<br/><br/>Indica si el tráfico se envía por HTTPS (si se configura en 1) o por HTTP (si se configura en 0). |
| `s:sp:ovp` | MediaHeartbeatConfig | (Opcional)<br/><br/>Establézcalo en “primetime” para reproductores de Primetime o en el OVP real para otros reproductores. |
| `s:sp:sdk` | MediaHeartbeatConfig | (Obligatorio)<br/><br/>La cadena de versión de OVP. |
| `s:sp:player_name` | VideoInfo | (Obligatorio)<br/><br/>El nombre del reproductor (el software del reproductor real, utilizado para identificar al mismo). |
| `s:sp:channel` | MediaHeartbeatConfig | (Opcional)<br/><br/>Canal donde el usuario ve el contenido. Para una aplicación móvil, el nombre de la aplicación. Para un sitio web, el nombre de dominio. |
| `s:sp:hb_version` | Media SDK | (Obligatorio)<br/><br/>El número de versión de la biblioteca de Media SDK que emite la llamada. |
| `l:stream:bitrate` | QoSInfo | (Obligatorio)<br/><br/>Valor real de la velocidad de bits de la emisión (en bps). |

## Eventos de error

| Nombre | Fuente de datos | Descripción   |
| ---  | --- | --- |
| `s:event:source` | Media SDK | (Obligatorio)<br/><br/>Origen del error, ya sea que esté en el reproductor o en la aplicación. |
| `s:event:id` | Media SDK | (Obligatorio)<br/><br/>ID de error que lo identifica de forma única. |

## Eventos de anuncio

| Nombre | Fuente de datos | Descripción   |
| ---  | --- | --- |
| `s:asset:ad_id` | AdInfo | (Obligatorio)<br/><br/>El nombre del anuncio. |
| `s:asset:ad_sid` | Media SDK | (Obligatorio)<br/><br/>Identificador único generado por el Media SDK, anexado a todos los pings relacionados con anuncios. |
| `s:asset:pod_id` | Media SDK | (Obligatorio)<br/><br/>ID de la secuencia dentro del vídeo. Este valor se calcula automáticamente en función de la siguiente fórmula: <br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| `s:asset:pod_position` | AdBreakInfo | (Obligatorio)<br/><br/>Índice del anuncio dentro de la secuencia (el primer anuncio tiene el índice 0, el segundo tiene el índice 1, etc.). |
| `s:asset:resolver` | AdBreakInfo | (Obligatorio)<br/><br/>La resolución del anuncio. |
| `s:meta:custom_ad_metadata.x` | MediaHeartbeat | (Opcional)<br/><br/>Los metadatos de anuncios personalizados. |

## Eventos de capítulo

| Nombre | Fuente de datos | Descripción   |
| ---  | --- | --- |
| `s:stream:chapter_sid` | Media SDK | (Obligatorio)<br/><br/>Identificador único asociado a la instancia de reproducción del capítulo.  <br/> **Nota:** Un capítulo se puede reproducir varias veces debido a las operaciones seek-back realizadas por el usuario. |
| `s:stream:chapter_name` | ChapterInfo | (Opcional)<br/><br/>El nombre descriptivo del capítulo (por ejemplo, que sea comprensible). |
| `s:stream:chapter_id` | Media SDK | (Obligatorio)<br/><br/>ID único del capítulo. Este valor se calcula automáticamente en función de la siguiente fórmula: <br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| `l:stream:chapter_pos` | ChapterInfo | (Obligatorio)<br/><br/>Índice del capítulo en la lista de capítulos (a partir del 1). |
| `l:stream:chapter_offset` | ChapterInfo | (Obligatorio)<br/><br/>El desplazamiento del capítulo (expresado en segundos) dentro del contenido principal, sin incluir los anuncios. |
| `l:stream:chapter_length` | ChapterInfo | (Obligatorio)<br/><br/>La duración del capítulo (expresada en segundos). |
| `s:meta:custom_chapter_metadata.x` | ChapterInfo | (Opcional)<br/><br/>Metadatos de capítulo personalizados. |

## Evento Fin de la sesión

| Nombre | Fuente de datos | Descripción   |
| ---  | --- | --- |
| `s:event:type=end` | Media SDK | (Obligatorio)<br/><br/> El `end` `close` |
